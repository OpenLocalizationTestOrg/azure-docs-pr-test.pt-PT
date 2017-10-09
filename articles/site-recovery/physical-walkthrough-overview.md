---
title: "aaaReplicate físicos no local tooAzure de servidores com o Azure Site Recovery | Microsoft Docs"
description: "Fornece uma descrição geral dos passos de Olá para replicar as cargas de trabalho em execução no tooAzure de servidores físicos Windows/Linux no local com Olá serviço Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a><span data-ttu-id="d9b7f-103">Replicar servidores físicos tooAzure com a recuperação de Site</span><span class="sxs-lookup"><span data-stu-id="d9b7f-103">Replicate physical servers tooAzure with Site Recovery</span></span>

<span data-ttu-id="d9b7f-104">Este artigo fornece uma descrição geral de Olá passos tooreplicate necessária no local Windows/Linux servidores físicos tooAzure, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-104">This article provides an overview of hello steps required tooreplicate on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="d9b7f-105">Passo 1: Rever pré-requisitos e arquitetura</span><span class="sxs-lookup"><span data-stu-id="d9b7f-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="d9b7f-106">Antes de iniciar a implementação, reveja a arquitetura do cenário de Olá e certifique-se de que compreende a todos os componentes de Olá tem tooset com a implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-106">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need tooset up hello deployment.</span></span>

<span data-ttu-id="d9b7f-107">Aceda demasiado[passo 1: rever a arquitetura de Olá](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="d9b7f-107">Go too[Step 1: Review hello architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="d9b7f-108">Passo 2: Pré-requisitos de revisão</span><span class="sxs-lookup"><span data-stu-id="d9b7f-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="d9b7f-109">Certifique-se de que tem os pré-requisitos de Olá local para cada componente de implementação:</span><span class="sxs-lookup"><span data-stu-id="d9b7f-109">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="d9b7f-110">**Pré-requisitos do Azure**: precisará de uma conta do Microsoft Azure, as redes do Azure e as contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="d9b7f-111">**Componentes da recuperação de Site local**: precisa de uma máquina com componentes da recuperação de Site no local.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="d9b7f-112">**Replicar máquinas**: tem de servidores que pretende tooreplicate toocomply no local e requisitos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-112">**Replicated machines**: Servers you want tooreplicate need toocomply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="d9b7f-113">Aceda demasiado[passo 2: consultar pré-requisitos e limitações](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="d9b7f-113">Go too[Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="d9b7f-114">Passo 3: Capacidade de plano</span><span class="sxs-lookup"><span data-stu-id="d9b7f-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="d9b7f-115">Se estiver a fazer uma implementação completa tem toofigure saída que recursos de replicação tem.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-115">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="d9b7f-116">Se estiver a fazer uma rápida configurar tootest Olá ambiente, pode ignorar este passo.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-116">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="d9b7f-117">Aceda demasiado[passo 3: planear a capacidade](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="d9b7f-117">Go too[Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="d9b7f-118">Passo 4: Planear o funcionamento em rede</span><span class="sxs-lookup"><span data-stu-id="d9b7f-118">Step 4: Plan networking</span></span>

<span data-ttu-id="d9b7f-119">É necessário toodo algum planeamento tooensure VMs do Azure são toonetworks ligado, após a ocorrência da ativação pós-falha, e que têm Olá direita endereços IP da rede.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-119">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="d9b7f-120">Aceda demasiado[passo 4: planear o funcionamento em rede](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="d9b7f-120">Go too[Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="d9b7f-121">Passo 5: Preparar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="d9b7f-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="d9b7f-122">Configure redes do Azure e de armazenamento antes de começar.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="d9b7f-123">Aceda demasiado[passo 5: preparar o Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="d9b7f-123">Go too[Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="d9b7f-124">Passo 6: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="d9b7f-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="d9b7f-125">Configurar um tooorchestrate do Cofre de serviços de recuperação e gerir a replicação.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-125">You set up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="d9b7f-126">Quando configurar o Cofre de Olá, especifique de que pretende tooreplicate, e onde pretende tooreplicate para.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-126">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="d9b7f-127">Aceda demasiado[passo 6: configurar um cofre](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="d9b7f-127">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="d9b7f-128">Passo 7: Configurar definições de origem e de destino</span><span class="sxs-lookup"><span data-stu-id="d9b7f-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="d9b7f-129">Configurar definições para Olá origem e destino site (Azure).</span><span class="sxs-lookup"><span data-stu-id="d9b7f-129">Configure settings for hello source and target (Azure) site.</span></span> <span data-ttu-id="d9b7f-130">Definições de origem inclui executar configuração Unified tooinstall componentes da recuperação de Site do Olá no local.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-130">Source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="d9b7f-131">Aceda demasiado[passo 7: Configurar Olá origem e de destino](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="d9b7f-131">Go too[Step 7: Set up hello source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="d9b7f-132">Passo 8: Configurar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="d9b7f-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="d9b7f-133">Configurar uma política toospecify físicos como servidores devem replicar.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-133">You set up a policy toospecify how physical servers should replicate.</span></span>

<span data-ttu-id="d9b7f-134">Aceda demasiado[passo 8: configurar uma política de replicação](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="d9b7f-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="d9b7f-135">Passo 9: Instalar o serviço de mobilidade Olá</span><span class="sxs-lookup"><span data-stu-id="d9b7f-135">Step 9: Install hello Mobility service</span></span>

<span data-ttu-id="d9b7f-136">Olá serviço de mobilidade tem de ser instalado em cada servidor que pretende tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-136">hello Mobility service must be installed on each server you want tooreplicate.</span></span> <span data-ttu-id="d9b7f-137">Existem algumas formas tooset serviço Olá, com a instalação de push ou pull.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-137">There are a few ways tooset up hello service, with push or pull installation.</span></span>

<span data-ttu-id="d9b7f-138">Aceda demasiado[passo 9: instalar o serviço de mobilidade Olá](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="d9b7f-138">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="d9b7f-139">Passo 10: Ativar a replicação</span><span class="sxs-lookup"><span data-stu-id="d9b7f-139">Step 10: Enable replication</span></span>

<span data-ttu-id="d9b7f-140">Depois de Olá serviço de mobilidade está em execução num servidor, pode ativar a replicação para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-140">After hello Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="d9b7f-141">Depois de ativar, ocorre a replicação inicial Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-141">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="d9b7f-142">Aceda demasiado[passo 10: Ativar a replicação](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="d9b7f-142">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="d9b7f-143">Passo 11: Executar uma ativação pós-falha de teste</span><span class="sxs-lookup"><span data-stu-id="d9b7f-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="d9b7f-144">Após a conclusão da replicação inicial e a replicação de diferenças está em execução, pode executar um toomake de ativação pós-falha de teste se de que tudo funciona conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="d9b7f-144">After initial replication finishes and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="d9b7f-145">Aceda demasiado[passo 11: executar uma ativação pós-falha de teste](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="d9b7f-145">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

