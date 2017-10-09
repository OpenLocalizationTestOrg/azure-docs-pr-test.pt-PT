---
title: "servidores de aaaRemove e desative a proteção | Microsoft Docs"
description: "Este artigo descreve como servidores de toounregister a partir de uma recuperação de Site do cofre e toodisable proteção para máquinas virtuais e servidores físicos."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="05cb2-103">Remover servidores e desativar proteção</span><span class="sxs-lookup"><span data-stu-id="05cb2-103">Remove servers and disable protection</span></span>

<span data-ttu-id="05cb2-104">Olá serviço Azure Site Recovery contribui tooyour continuidade do negócio e a estratégia de recuperação (BCDR) de desastre.</span><span class="sxs-lookup"><span data-stu-id="05cb2-104">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="05cb2-105">serviço de Olá orquestra a replicação, ativação pós-falha e recuperação de máquinas virtuais e servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="05cb2-105">hello service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="05cb2-106">As máquinas podem ser replicada tooAzure ou centro de dados do tooa secundário no local.</span><span class="sxs-lookup"><span data-stu-id="05cb2-106">Machines can be replicated tooAzure, or tooa secondary on-premises data center.</span></span> <span data-ttu-id="05cb2-107">Para uma descrição geral, leia [O que é o Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="05cb2-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="05cb2-108">Este artigo descreve como servidores de toounregister nos serviços de recuperação do cofre no Olá portal do Azure e como toodisable proteção para máquinas protegidas pela recuperação de sites.</span><span class="sxs-lookup"><span data-stu-id="05cb2-108">This article describes how toounregister servers from a Recovery Services vault in hello Azure portal, and how toodisable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="05cb2-109">Publique comentários ou perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="05cb2-109">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="05cb2-110">Anular o registo de um servidor de configuração ligada</span><span class="sxs-lookup"><span data-stu-id="05cb2-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="05cb2-111">Se replicar VMs de VMware ou tooAzure de servidores físicos Windows/Linux, pode anular registo um servidor de configuração ligada de um cofre da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="05cb2-111">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="05cb2-112">Desative a proteção da máquina.</span><span class="sxs-lookup"><span data-stu-id="05cb2-112">Disable machine protection.</span></span> <span data-ttu-id="05cb2-113">No **itens protegidos** > **itens replicados**, máquina do contexto Olá > **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-113">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="05cb2-114">Desassocie todas as políticas.</span><span class="sxs-lookup"><span data-stu-id="05cb2-114">Disassociate any policies.</span></span> <span data-ttu-id="05cb2-115">No **infraestrutura de recuperação de Site** > **para VMWare e máquinas físicas** > **políticas de replicação**, faça duplo clique em Olá política associada.</span><span class="sxs-lookup"><span data-stu-id="05cb2-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="05cb2-116">Servidor de configuração do contexto Olá > **Disassociate**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-116">Right-click hello configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="05cb2-117">Remova quaisquer processos adicionais no local ou servidores de destino principal.</span><span class="sxs-lookup"><span data-stu-id="05cb2-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="05cb2-118">No **infraestrutura de recuperação de Site** > **para VMWare e máquinas físicas** > **servidores de configuração**, servidor de Olá de contexto > **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="05cb2-119">Elimine o servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-119">Delete hello configuration server.</span></span>
5. <span data-ttu-id="05cb2-120">Desinstale manualmente o serviço de mobilidade de Olá em execução no servidor de destino mestre Olá (isto será um separado ou servidor ou em execução no servidor de configuração de Olá).</span><span class="sxs-lookup"><span data-stu-id="05cb2-120">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
6. <span data-ttu-id="05cb2-121">Desinstale todos os servidores adicionais do processo.</span><span class="sxs-lookup"><span data-stu-id="05cb2-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="05cb2-122">Desinstale o servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-122">Uninstall hello configuration server.</span></span>
8. <span data-ttu-id="05cb2-123">No servidor de configuração de Olá, desinstale instância Olá MySQL que tenha sido instalado pelo Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="05cb2-123">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="05cb2-124">No registo de hello do servidor de configuração de Olá eliminar a chave de Olá ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="05cb2-124">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="05cb2-125">Anular o registo de um servidor de configuração desligado</span><span class="sxs-lookup"><span data-stu-id="05cb2-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="05cb2-126">Se replicar VMs de VMware ou tooAzure de servidores físicos Windows/Linux, pode anular registo um servidor de configuração desligado de um cofre da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="05cb2-126">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="05cb2-127">Desative a proteção da máquina.</span><span class="sxs-lookup"><span data-stu-id="05cb2-127">Disable machine protection.</span></span> <span data-ttu-id="05cb2-128">No **itens protegidos** > **itens replicados**, máquina do contexto Olá > **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-128">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span> <span data-ttu-id="05cb2-129">Selecione **parar de gerir a máquina Olá**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-129">Select **Stop managing hello machine**.</span></span>
2. <span data-ttu-id="05cb2-130">Remova quaisquer processos adicionais no local ou servidores de destino principal.</span><span class="sxs-lookup"><span data-stu-id="05cb2-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="05cb2-131">No **infraestrutura de recuperação de Site** > **para VMWare e máquinas físicas** > **servidores de configuração**, servidor de Olá de contexto > **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
3. <span data-ttu-id="05cb2-132">Elimine o servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-132">Delete hello configuration server.</span></span>
4. <span data-ttu-id="05cb2-133">Desinstale manualmente o serviço de mobilidade de Olá em execução no servidor de destino mestre Olá (isto será um separado ou servidor ou em execução no servidor de configuração de Olá).</span><span class="sxs-lookup"><span data-stu-id="05cb2-133">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
5. <span data-ttu-id="05cb2-134">Desinstale todos os servidores adicionais do processo.</span><span class="sxs-lookup"><span data-stu-id="05cb2-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="05cb2-135">Desinstale o servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-135">Uninstall hello configuration server.</span></span>
7. <span data-ttu-id="05cb2-136">No servidor de configuração de Olá, desinstale instância Olá MySQL que tenha sido instalado pelo Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="05cb2-136">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="05cb2-137">No registo de hello do servidor de configuração de Olá eliminar a chave de Olá ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="05cb2-137">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="05cb2-138">Anular o registo de um ligado ao servidor do VMM</span><span class="sxs-lookup"><span data-stu-id="05cb2-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="05cb2-139">Como melhor prática, recomendamos que pode anular o registo do servidor do VMM Olá quando estabeleceu tooAzure.</span><span class="sxs-lookup"><span data-stu-id="05cb2-139">As a best practice, we recommend that you unregister hello VMM server when it's connected tooAzure.</span></span> <span data-ttu-id="05cb2-140">Isto garante que limpar as definições nos servidores do VMM Olá (e noutros servidores do VMM com nuvens emparelhadas) são corretamente.</span><span class="sxs-lookup"><span data-stu-id="05cb2-140">This ensures that settings on hello VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="05cb2-141">Só deve remover um servidor de desligado, se existir um problema com conectividade permanente.</span><span class="sxs-lookup"><span data-stu-id="05cb2-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="05cb2-142">Se o servidor do VMM Olá não está ligado, será necessário toomanually executar tooclean um script das definições.</span><span class="sxs-lookup"><span data-stu-id="05cb2-142">If hello VMM server isn’t connected, you will need toomanually run a script tooclean up settings.</span></span>

1. <span data-ttu-id="05cb2-143">Pare a replicar VMs em nuvens no Olá pretende tooremove de servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="05cb2-143">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="05cb2-144">Elimine quaisquer mapeamentos de rede utilizados pelo nuvens no Olá pretende toodelete de servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="05cb2-144">Delete any network mappings used by clouds on hello VMM server you want toodelete.</span></span> <span data-ttu-id="05cb2-145">No **infraestrutura de recuperação de Site** > **para o System Center VMM** > **mapeamento da rede**, faça duplo clique mapeamento da rede Olá >  **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="05cb2-146">Desassocie políticas de replicação das nuvens no Olá pretende tooremove de servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="05cb2-146">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="05cb2-147">No **infraestrutura de recuperação de Site** > **para o System Center VMM** >  **políticas de replicação**, faça duplo clique Olá associado à política.</span><span class="sxs-lookup"><span data-stu-id="05cb2-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="05cb2-148">Faça duplo clique na nuvem de Olá > **Disassociate**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-148">Right-click hello cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="05cb2-149">Elimine o servidor do VMM Olá ou o nó ativo do VMM.</span><span class="sxs-lookup"><span data-stu-id="05cb2-149">Delete hello VMM server or active VMM node.</span></span> <span data-ttu-id="05cb2-150">No **infraestrutura de recuperação de Site** > **para o System Center VMM** > **servidores VMM**, servidor de Olá contexto >  **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
5. <span data-ttu-id="05cb2-151">Desinstale Olá fornecedor manualmente no servidor do VMM Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-151">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="05cb2-152">Se tiver um cluster, remova todos os nós.</span><span class="sxs-lookup"><span data-stu-id="05cb2-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="05cb2-153">Se estiver a replicar tooAzure, remova manualmente o agente de serviços de recuperação do Microsoft de Olá dos anfitriões Hyper-V em nuvens Olá eliminado.</span><span class="sxs-lookup"><span data-stu-id="05cb2-153">If you're replicating tooAzure, manually remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="05cb2-154">Anular o registo de um servidor VMM desligado</span><span class="sxs-lookup"><span data-stu-id="05cb2-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="05cb2-155">Pare a replicar VMs em nuvens no Olá pretende tooremove de servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="05cb2-155">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="05cb2-156">Elimine quaisquer mapeamentos de rede utilizados pelo nuvens no servidor do VMM Olá que pretende que o toodelete.</span><span class="sxs-lookup"><span data-stu-id="05cb2-156">Delete any network mappings used by clouds on hello VMM server that you want toodelete.</span></span> <span data-ttu-id="05cb2-157">No **infraestrutura de recuperação de Site** > **para o System Center VMM** > **mapeamento da rede**, faça duplo clique mapeamento da rede Olá >  **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="05cb2-158">Tenha em atenção Olá ID hello do servidor de VMM.</span><span class="sxs-lookup"><span data-stu-id="05cb2-158">Note hello ID of hello VMM server.</span></span>
4. <span data-ttu-id="05cb2-159">Desassocie políticas de replicação das nuvens no Olá pretende tooremove de servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="05cb2-159">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="05cb2-160">No **infraestrutura de recuperação de Site** > **para o System Center VMM** >  **políticas de replicação**, faça duplo clique Olá associado à política.</span><span class="sxs-lookup"><span data-stu-id="05cb2-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="05cb2-161">Faça duplo clique na nuvem de Olá > **Disassociate**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-161">Right-click hello cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="05cb2-162">Elimine o servidor do VMM Olá ou o nó ativo.</span><span class="sxs-lookup"><span data-stu-id="05cb2-162">Delete hello VMM server or active node.</span></span> <span data-ttu-id="05cb2-163">No **infraestrutura de recuperação de Site** > **para o System Center VMM** > **servidores VMM**, servidor de Olá contexto >  **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
6. <span data-ttu-id="05cb2-164">Transferir e executar Olá [script de limpeza](http://aka.ms/asr-cleanup-script-vmm) no servidor do VMM Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-164">Download and run hello [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on hello VMM server.</span></span> <span data-ttu-id="05cb2-165">Abra o PowerShell com Olá **executar como administrador** opção, a política de execução de Olá toochange para âmbito do Olá predefinido (LocalMachine).</span><span class="sxs-lookup"><span data-stu-id="05cb2-165">Open PowerShell with hello **Run as Administrator** option, toochange hello execution policy for hello default (LocalMachine) scope.</span></span> <span data-ttu-id="05cb2-166">No script de Olá, especifique o ID de Olá de Olá pretende tooremove de servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="05cb2-166">In hello script, specify hello ID of hello VMM server you want tooremove.</span></span> <span data-ttu-id="05cb2-167">script de Olá remove informações do servidor de Olá de emparelhamento da nuvem e de registo.</span><span class="sxs-lookup"><span data-stu-id="05cb2-167">hello script removes registration and cloud pairing information from hello server.</span></span>
5. <span data-ttu-id="05cb2-168">Execute script de limpeza de Olá noutros servidores do VMM que contêm as nuvens que estão associadas a nuvens no Olá pretende tooremove de servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="05cb2-168">Run hello cleanup script on any other VMM servers that contain clouds that are paired with clouds on hello VMM server you want tooremove.</span></span>
6. <span data-ttu-id="05cb2-169">Execute script de limpeza de Olá em qualquer outros passivos VMM nós de cluster que tenham Olá que fornecedor instalado.</span><span class="sxs-lookup"><span data-stu-id="05cb2-169">Run hello  cleanup script on any other passive VMM cluster nodes that have hello Provider installed.</span></span>
7. <span data-ttu-id="05cb2-170">Desinstale Olá fornecedor manualmente no servidor do VMM Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-170">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="05cb2-171">Se tiver um cluster, remova todos os nós.</span><span class="sxs-lookup"><span data-stu-id="05cb2-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="05cb2-172">Se replicar tooAzure, pode remover agente de serviços de recuperação do Microsoft Olá dos anfitriões Hyper-V em nuvens Olá eliminado.</span><span class="sxs-lookup"><span data-stu-id="05cb2-172">If you replicating tooAzure, you can remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="05cb2-173">Anular o registo de um anfitrião de Hyper-V num Site Hyper-V</span><span class="sxs-lookup"><span data-stu-id="05cb2-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="05cb2-174">Anfitriões Hyper-V que não são geridas pelo VMM foram recolhidas para um site de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="05cb2-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="05cb2-175">Remova um anfitrião num site Hyper-V da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="05cb2-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="05cb2-176">Desative a replicação para as VMs de Hyper-V localizada num anfitrião Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-176">Disable replication for Hyper-V VMs located on hello host.</span></span>
2. <span data-ttu-id="05cb2-177">Desassocie políticas para o site de Hyper-V Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-177">Disassociate policies for hello Hyper-V site.</span></span> <span data-ttu-id="05cb2-178">No **infraestrutura de recuperação de Site** > **para Sites de Hyper-V** >  **políticas de replicação**, faça duplo clique Olá associado à política.</span><span class="sxs-lookup"><span data-stu-id="05cb2-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="05cb2-179">Site do contexto Olá > **Disassociate**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-179">Right-click hello site > **Disassociate**.</span></span>
3. <span data-ttu-id="05cb2-180">Elimine anfitriões Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="05cb2-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="05cb2-181">No **infraestrutura de recuperação de Site** > **para o System Center VMM** > **anfitriões Hyper-V**, servidor de Olá contexto >  **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="05cb2-182">Elimine o site de Olá Hyper-V depois de todos os anfitriões foram removidos do mesmo.</span><span class="sxs-lookup"><span data-stu-id="05cb2-182">Delete hello Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="05cb2-183">No **infraestrutura de recuperação de Site** > **para o System Center VMM** > **Sites Hyper-V**, site do contexto Olá >  **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click hello site > **Delete**.</span></span>
5. <span data-ttu-id="05cb2-184">Execute o seguinte script em cada anfitrião de Hyper-V que removeu de Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-184">Run hello following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="05cb2-185">script de Olá limpa as definições no servidor de Olá e anula o registo do Cofre de Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-185">hello script cleans up settings on hello server, and unregisters it from hello vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="05cb2-186">Desative a proteção para uma VM de VMware ou o servidor físico</span><span class="sxs-lookup"><span data-stu-id="05cb2-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="05cb2-187">No **itens protegidos** > **itens replicados**, máquina do contexto Olá > **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-187">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="05cb2-188">No **remover máquina**, selecione uma destas opções:</span><span class="sxs-lookup"><span data-stu-id="05cb2-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="05cb2-189">**Desative a proteção da máquina de Olá (recomendada)**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-189">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="05cb2-190">Utilize este toostop opção máquina Olá a replicar.</span><span class="sxs-lookup"><span data-stu-id="05cb2-190">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="05cb2-191">Definições de recuperação de site serão limpa automaticamente.</span><span class="sxs-lookup"><span data-stu-id="05cb2-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="05cb2-192">Apenas será apresentada esta opção no Olá seguintes circunstâncias:</span><span class="sxs-lookup"><span data-stu-id="05cb2-192">You will only see this option in hello following circumstances:</span></span>
        - <span data-ttu-id="05cb2-193">**Foi redimensionado volume VM Olá**— quando redimensionar um Olá volume virtual máquina entra no estado crítico.</span><span class="sxs-lookup"><span data-stu-id="05cb2-193">**You've resized hello VM volume**—When you resize a volume hello virtual machine goes into a critical state.</span></span> <span data-ttu-id="05cb2-194">Selecione esta proteção de toodisables opção, mantendo o pontos de recuperação no Azure.</span><span class="sxs-lookup"><span data-stu-id="05cb2-194">Select this option toodisables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="05cb2-195">Quando ativar a proteção da máquina de Olá novamente, Olá para volume Olá redimensionado serão dados tooAzure transferido.</span><span class="sxs-lookup"><span data-stu-id="05cb2-195">When you enable protection for hello machine again, hello data for hello resized volume will be transferred tooAzure.</span></span>
        - <span data-ttu-id="05cb2-196">**Recentemente tiver executar uma ativação pós-falha**— após executar uma ativação pós-falha tootest seu ambiente, selecione toostart esta opção proteger novamente máquinas no local.</span><span class="sxs-lookup"><span data-stu-id="05cb2-196">**You've recently run a failover**—After you've run a failover tootest your environment, select this option toostart protecting on-premises machines again.</span></span> <span data-ttu-id="05cb2-197">Desativa a cada máquina virtual e, em seguida, terá proteção tooenable para os mesmos novamente.</span><span class="sxs-lookup"><span data-stu-id="05cb2-197">It disables each virtual machine, and then you need tooenable protection for them again.</span></span> <span data-ttu-id="05cb2-198">A desativação Olá máquina com esta definição não afeta a máquina virtual de réplica de Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="05cb2-198">Disabling hello machine with this setting doesn't affect hello replica virtual machine in Azure.</span></span> <span data-ttu-id="05cb2-199">Não desinstale o serviço de mobilidade Olá da máquina de Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-199">Don't uninstall hello Mobility service from hello machine.</span></span>
    - <span data-ttu-id="05cb2-200">**Parar de gerir a máquina Olá**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-200">**Stop managing hello machine**.</span></span> <span data-ttu-id="05cb2-201">Se selecionar esta opção, máquina Olá só será removida do Cofre de Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-201">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="05cb2-202">As definições de proteção no local para a máquina Olá não serão afetadas.</span><span class="sxs-lookup"><span data-stu-id="05cb2-202">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="05cb2-203">tooremove definições na máquina de Olá e a máquina de Olá tooremove do Olá subscrição do Azure, terá das definições de Olá tooclean por desinstalar o serviço de mobilidade Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-203">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings by uninstalling hello Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="05cb2-204">Desative a proteção para uma VM de Hyper-V numa nuvem VMM</span><span class="sxs-lookup"><span data-stu-id="05cb2-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="05cb2-205">No **itens protegidos** > **itens replicados**, máquina do contexto Olá > **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-205">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="05cb2-206">No **remover máquina**, selecione uma destas opções:</span><span class="sxs-lookup"><span data-stu-id="05cb2-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="05cb2-207">**Desative a proteção da máquina de Olá (recomendada)**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-207">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="05cb2-208">Utilize este toostop opção máquina Olá a replicar.</span><span class="sxs-lookup"><span data-stu-id="05cb2-208">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="05cb2-209">Definições de recuperação de site serão limpa automaticamente.</span><span class="sxs-lookup"><span data-stu-id="05cb2-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="05cb2-210">**Parar de gerir a máquina Olá**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-210">**Stop managing hello machine**.</span></span> <span data-ttu-id="05cb2-211">Se selecionar esta opção, máquina Olá só será removida do Cofre de Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-211">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="05cb2-212">As definições de proteção no local para a máquina Olá não serão afetadas.</span><span class="sxs-lookup"><span data-stu-id="05cb2-212">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="05cb2-213">tooremove definições na máquina de Olá e a máquina de Olá tooremove do Olá subscrição do Azure, terá das definições de Olá tooclean cópias de segurança manualmente, utilizando instruções Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="05cb2-213">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings up manually, using hello instructions below.</span></span> <span data-ttu-id="05cb2-214">Tenha em atenção que se selecionar toodelete Olá máquina e os respetivos discos rígidos, irá ser removidos do localização de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-214">Note that if you select toodelete hello virtual machine and its hard disks, they'll be removed from hello target location.</span></span>

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a><span data-ttu-id="05cb2-215">Limpar as definições de proteção - replicação tooa site secundário do VMM</span><span class="sxs-lookup"><span data-stu-id="05cb2-215">Clean up protection settings - replication tooa secondary VMM site</span></span>

<span data-ttu-id="05cb2-216">Se tiver selecionado **parar de gerir a máquina Olá** e pode replicar tooa o site secundário, execute este script no servidor primário de Olá tooclean segurança Olá as definições de máquina virtual primária de Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-216">If you selected **Stop managing hello machine** and you replicating tooa secondary site, run this script on hello primary server tooclean up hello settings for hello primary virtual machine.</span></span> <span data-ttu-id="05cb2-217">Na consola do VMM Olá clique consola do VMM PowerShell de Olá tooopen Olá PowerShell botão.</span><span class="sxs-lookup"><span data-stu-id="05cb2-217">In hello VMM console click hello PowerShell button tooopen hello VMM PowerShell console.</span></span> <span data-ttu-id="05cb2-218">Substitua SQLVM1 com o nome de Olá da sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="05cb2-218">Replace SQLVM1 with hello name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="05cb2-219">Servidor do VMM secundário Olá execute tooclean este script segurança Olá as definições de máquina virtual secundária de Olá:</span><span class="sxs-lookup"><span data-stu-id="05cb2-219">On hello secondary VMM server run this script tooclean up hello settings for hello secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="05cb2-220">Olá VMM do servidor secundário, atualize Olá máquinas de virtuais no servidor de anfitrião de Hyper-V Olá, para que hello VM secundário obtém detetado novamente na consola do VMM Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-220">On hello secondary VMM server, refresh hello virtual machines on hello Hyper-V host server, so that hello secondary VM gets detected again in hello VMM console.</span></span>
4. <span data-ttu-id="05cb2-221">Olá os passos acima limpar as definições de replicação de Olá no servidor do VMM Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-221">hello above steps clear up hello replication settings on hello VMM server.</span></span> <span data-ttu-id="05cb2-222">Se pretender que a replicação da máquina virtual de Olá, execute o seguinte script esqueceu de Olá toostop Olá VMs primários e secundários.</span><span class="sxs-lookup"><span data-stu-id="05cb2-222">If you want toostop replication for hello virtual machine, run hello following script oh hello primary and secondary VMs.</span></span> <span data-ttu-id="05cb2-223">Substitua SQLVM1 com o nome de Olá da sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="05cb2-223">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a><span data-ttu-id="05cb2-224">Limpar as definições de proteção - tooAzure de replicação</span><span class="sxs-lookup"><span data-stu-id="05cb2-224">Clean up protection settings - replication tooAzure</span></span>

1. <span data-ttu-id="05cb2-225">Se tiver selecionado **parar de gerir a máquina Olá** e replicar tooAzure, execute este script no servidor VMM de origem Olá, utilizando o PowerShell a partir da consola do VMM Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-225">If you selected **Stop managing hello machine** and you replicate tooAzure, run this script on hello source VMM server, using PowerShell from hello VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="05cb2-226">Olá os passos acima limpar as definições de replicação de Olá no servidor do VMM Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-226">hello above steps clear hello replication settings on hello VMM server.</span></span> <span data-ttu-id="05cb2-227">toostop replicação da máquina virtual de Olá em execução no servidor de anfitrião de Hyper-V Olá, execute este script.</span><span class="sxs-lookup"><span data-stu-id="05cb2-227">toostop replication for hello virtual machine running on hello Hyper-V host server, run this script.</span></span> <span data-ttu-id="05cb2-228">Substitua SQLVM1 nome Olá da sua máquina virtual e host01.contoso.com com o nome de Olá Olá Hyper-V do servidor de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="05cb2-228">Replace SQLVM1 with hello name of your virtual machine, and host01.contoso.com with hello name of hello Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="05cb2-229">Desative a proteção para uma VM de Hyper-V num Site Hyper-V</span><span class="sxs-lookup"><span data-stu-id="05cb2-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="05cb2-230">Utilize este procedimento se está a replicar VMs Hyper-V tooAzure sem um servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="05cb2-230">Use this procedure if you're replicating Hyper-V VMs tooAzure without a VMM server.</span></span>

1. <span data-ttu-id="05cb2-231">No **itens protegidos** > **itens replicados**, máquina do contexto Olá > **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-231">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="05cb2-232">No **remover máquina**, pode selecionar Olá seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="05cb2-232">In **Remove Machine**, you can select hello following options:</span></span>

   - <span data-ttu-id="05cb2-233">**Desative a proteção da máquina de Olá (recomendada)**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-233">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="05cb2-234">Utilize este toostop opção máquina Olá a replicar.</span><span class="sxs-lookup"><span data-stu-id="05cb2-234">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="05cb2-235">Definições de recuperação de site serão limpa automaticamente.</span><span class="sxs-lookup"><span data-stu-id="05cb2-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="05cb2-236">**Parar de gerir a máquina Olá**.</span><span class="sxs-lookup"><span data-stu-id="05cb2-236">**Stop managing hello machine**.</span></span> <span data-ttu-id="05cb2-237">Se selecionar esta opção máquina Olá só será removida do Cofre de Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-237">If you select this option hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="05cb2-238">As definições de proteção no local para a máquina Olá não serão afetadas.</span><span class="sxs-lookup"><span data-stu-id="05cb2-238">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="05cb2-239">definições de tooremove máquina Olá e tooremove Olá excluir máquina virtual de Olá subscrição do Azure, terá das definições de Olá tooclean cópias de segurança manualmente.</span><span class="sxs-lookup"><span data-stu-id="05cb2-239">tooremove settings on hello machine, and tooremove hello virtual machine from hello Azure subscription, you need tooclean hello settings up manually.</span></span> <span data-ttu-id="05cb2-240">Se selecionar toodelete Olá máquina e os respetivos discos rígidos serão removidos da localização de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-240">If you select toodelete hello virtual machine and its hard disks they will be removed from hello target location.</span></span>
3. <span data-ttu-id="05cb2-241">Se tiver selecionado **parar de gerir a máquina Olá**, execute este script no servidor de anfitrião do Hyper-V de origem Olá, tooremove replicação da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="05cb2-241">If you selected **Stop managing hello machine**, run this script on hello source Hyper-V host server, tooremove replication for hello virtual machine.</span></span> <span data-ttu-id="05cb2-242">Substitua SQLVM1 com o nome de Olá da sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="05cb2-242">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
