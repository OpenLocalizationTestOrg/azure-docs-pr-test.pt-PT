---
title: aaaMigrate VMs do AWS tooAzure | Microsoft Docs
description: "Este artigo descreve como toomigrate virtual máquinas em execução no tooAzure Amazon Web Services (AWS) utilizando o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a><span data-ttu-id="c7923-103">Migrar máquinas virtuais no tooAzure Amazon Web Services (AWS) com o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="c7923-103">Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery</span></span>

<span data-ttu-id="c7923-104">Este artigo descreve como toomigrate Windows em AWS instâncias máquinas de virtuais tooAzure com Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="c7923-104">This article describes how toomigrate AWS Windows instances tooAzure virtual machines with hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="c7923-105">Migração de forma eficaz é uma ativação pós-falha do AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c7923-105">Migration is effectively a failover from AWS tooAzure.</span></span> <span data-ttu-id="c7923-106">Não é possível tooAWS de máquinas de reativação pós-falha, e não existe nenhuma replicação em curso.</span><span class="sxs-lookup"><span data-stu-id="c7923-106">You can't failback machines tooAWS, and there's no ongoing replication.</span></span> <span data-ttu-id="c7923-107">Este artigo descreve Olá passos de migração no Olá portal do Azure e baseiam-se as instruções de Olá para [replicar um tooAzure de máquina física](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="c7923-107">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for [replicating a physical machine tooAzure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="c7923-108">Publique comentários ou perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="c7923-108">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="c7923-109">Sistemas operativos suportados</span><span class="sxs-lookup"><span data-stu-id="c7923-109">Supported operating systems</span></span>

<span data-ttu-id="c7923-110">Recuperação de sites pode ser instâncias utilizado toomigrate EC2 com qualquer uma das Olá os seguintes sistemas operativos:</span><span class="sxs-lookup"><span data-stu-id="c7923-110">Site Recovery can be used toomigrate EC2 instances running any of hello following operating systems:</span></span>

- <span data-ttu-id="c7923-111">Windows (apenas 64 bits)</span><span class="sxs-lookup"><span data-stu-id="c7923-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="c7923-112">Windows Server 2008 R2 SP1 + (controladores do Citrix PV ou apenas os controladores de AWS PV.</span><span class="sxs-lookup"><span data-stu-id="c7923-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="c7923-113">**As instâncias em execução controladores de VM de RedHat PV não são suportadas**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c7923-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="c7923-114">Linux (apenas 64 bits)</span><span class="sxs-lookup"><span data-stu-id="c7923-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="c7923-115">Red Hat Enterprise Linux 6.7 (apenas para instâncias HVM virtualizada)</span><span class="sxs-lookup"><span data-stu-id="c7923-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7923-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c7923-116">Prerequisites</span></span>

<span data-ttu-id="c7923-117">Eis o que precisa para esta implementação:</span><span class="sxs-lookup"><span data-stu-id="c7923-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="c7923-118">**Servidor de configuração**: um Amazon EC2 implementação da VM com o Windows Server 2012 R2 como servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="c7923-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as hello configuration server.</span></span> <span data-ttu-id="c7923-119">Por predefinição, hello outros componentes do Azure Site Recovery (servidor de processos e o servidor de destino principal) são instalados quando implementar o servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="c7923-119">By default, hello other Azure Site Recovery components (process server and master target server) are installed when you deploy hello configuration server.</span></span> <span data-ttu-id="c7923-120">Este artigo descreve Olá passos de migração no Olá portal do Azure e baseiam-se as instruções de Olá para [Saiba mais](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="c7923-120">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="c7923-121">**Instâncias de EC2**: Olá Amazon EC2 instâncias de máquinas virtuais que pretende que o toomigrate.</span><span class="sxs-lookup"><span data-stu-id="c7923-121">**EC2 instances**: hello Amazon EC2 virtual machines instances that you want toomigrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="c7923-122">Passos da implementação</span><span class="sxs-lookup"><span data-stu-id="c7923-122">Deployment steps</span></span>

1. <span data-ttu-id="c7923-123">Crie um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="c7923-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="c7923-124">Olá, grupo de segurança das suas instâncias EC2 deve ter regras configuradas tooallow comunicação entre a instância de EC2 Olá que pretende que o toomigrate e instância Olá no qual planeia toodeploy Olá servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="c7923-124">hello Security Group of your EC2 instances should have rules configured tooallow communication between hello EC2 instance that you want toomigrate, and hello instance on which you plan toodeploy hello Configuration Server.</span></span>

3. <span data-ttu-id="c7923-125">No Olá mesmo Amazon Virtual nuvem privada como as instâncias de EC2, implementar um servidor de configuração de ASR.</span><span class="sxs-lookup"><span data-stu-id="c7923-125">On hello same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="c7923-126">Consulte Olá VMware / físico tooAzure pré-requisitos de requisitos de implementação do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="c7923-126">Refer hello VMware / Physical tooAzure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="c7923-128">Depois do servidor de configuração é implementado no AWS e registado com o Cofre dos serviços de recuperação, deverá ver o servidor de configuração de Olá e servidor de processos em infraestrutura de recuperação de sites como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="c7923-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see hello configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="c7923-130">Após implementar o servidor de configuração de Olá (poderá demorar até too15 minustes para o mesmo tooappear), validar que este consegue comunicar com Olá VMs que pretende que o toomigrate.</span><span class="sxs-lookup"><span data-stu-id="c7923-130">After you've deployed hello configuration server (it might take up too15 minustes for it tooappear), validate that it can communicate with hello VMs that you want toomigrate.</span></span>

6. <span data-ttu-id="c7923-131">[Configurar as definições de replicação](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="c7923-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="c7923-132">Ativar a replicação: Ativar a replicação para Olá VMs que pretende toomigrate.</span><span class="sxs-lookup"><span data-stu-id="c7923-132">Enable replication: Enable replication for hello VMs you want toomigrate.</span></span> <span data-ttu-id="c7923-133">Pode detetar instâncias de EC2 Olá utilizando endereços IP privados Olá, que pode obter a partir da consola de EC2 Olá.</span><span class="sxs-lookup"><span data-stu-id="c7923-133">You can discover hello EC2 instances using hello private IP addresses, which you can get from hello EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="c7923-135">Depois de instâncias de Olá EC2 tenham sido protegidas e Olá replicação tooAzure estiver concluída, [executar uma ativação pós-falha de teste](site-recovery-test-failover-to-azure.md) toovalidate desempenho da sua aplicação no Azure.</span><span class="sxs-lookup"><span data-stu-id="c7923-135">Once hello EC2 instances have been protected and hello replication tooAzure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) toovalidate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="c7923-137">Execute uma ativação pós-falha do AWS tooAzure para cada VM.</span><span class="sxs-lookup"><span data-stu-id="c7923-137">Run a Failover from AWS tooAzure for each VM.</span></span> <span data-ttu-id="c7923-138">Opcionalmente, pode criar um plano de recuperação e executar uma ativação pós-falha, toomigrate várias máquinas virtuais do AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c7923-138">Optionally, you can create a recovery plan and run a Failover, toomigrate multiple virtual machines from AWS tooAzure.</span></span> <span data-ttu-id="c7923-139">[Saiba mais](site-recovery-create-recovery-plans.md) sobre os planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="c7923-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="c7923-140">Para a migração, não precisa de toocommit uma ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="c7923-140">For migration, you don't need toocommit a failover.</span></span> <span data-ttu-id="c7923-141">Em vez disso, selecione a opção de concluir a migração de Olá para cada máquina que pretende toomigrate.</span><span class="sxs-lookup"><span data-stu-id="c7923-141">Instead, you select hello Complete Migration option for each machine you want toomigrate.</span></span> <span data-ttu-id="c7923-142">Olá ação de concluir a migração conclusão do processo de migração de Olá, remove a replicação da máquina de Olá e deixa de recuperação de sites para a máquina Olá de faturação.</span><span class="sxs-lookup"><span data-stu-id="c7923-142">hello Complete Migration action finishes up hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

    ![Migrar](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="c7923-144">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c7923-144">Next steps</span></span>

- <span data-ttu-id="c7923-145">[Preparar máquinas migradas tooenable replicação](site-recovery-azure-to-azure-after-migration.md) tooanother região para as necessidades de recuperação após desastre.</span><span class="sxs-lookup"><span data-stu-id="c7923-145">[Prepare migrated machines tooenable replication](site-recovery-azure-to-azure-after-migration.md) tooanother region for disaster recovery needs.</span></span>
- <span data-ttu-id="c7923-146">Comece a proteger as suas cargas de trabalho ao [replicar máquinas virtuais do Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="c7923-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
