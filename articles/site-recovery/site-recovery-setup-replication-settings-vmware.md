---
title: "aaaSet das definições de replicação para o Azure Site Recovery | Microsoft Docs"
description: "Descreve como toodeploy recuperação de Site tooorchestrate replicação, ativação pós-falha e recuperação de VMs de Hyper-V no VMM como nuvens tooAzure."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a><span data-ttu-id="3d545-103">Gerir a política de replicação para tooAzure de VMware</span><span class="sxs-lookup"><span data-stu-id="3d545-103">Manage replication policy for VMware tooAzure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="3d545-104">Criar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="3d545-104">Create a replication policy</span></span>

1. <span data-ttu-id="3d545-105">Selecione **Gerir** > **Infraestrutura do Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="3d545-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="3d545-106">Selecione **Políticas de replicação** em **Para VMware e Máquinas físicas**.</span><span class="sxs-lookup"><span data-stu-id="3d545-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="3d545-107">Selecione **+Política de replicação**.</span><span class="sxs-lookup"><span data-stu-id="3d545-107">Select **+Replication policy**.</span></span>

    ![Criar política de replicação](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="3d545-109">Introduza o nome da política Olá.</span><span class="sxs-lookup"><span data-stu-id="3d545-109">Enter hello policy name.</span></span>

5. <span data-ttu-id="3d545-110">No **limiar RPO**, especificar Olá RPO limite.</span><span class="sxs-lookup"><span data-stu-id="3d545-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="3d545-111">Serão gerados alertas quando a replicação contínua exceder este limite.</span><span class="sxs-lookup"><span data-stu-id="3d545-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="3d545-112">No **retenção do ponto de recuperação**, especifique (em horas) Olá duração da janela de retenção de Olá para cada ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="3d545-112">In **Recovery point retention**, specify (in hours) hello duration of hello retention window for each recovery point.</span></span> <span data-ttu-id="3d545-113">Máquinas protegidas podem ser recuperados tooany ponto dentro de uma janela de retenção.</span><span class="sxs-lookup"><span data-stu-id="3d545-113">Protected machines can be recovered tooany point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3d545-114">Horas de too24 de retenção de cópias de segurança são suportadas para máquinas toopremium replicadas armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3d545-114">Up too24 hours of retention is supported for machines replicated toopremium storage.</span></span> <span data-ttu-id="3d545-115">Horas de too72 de retenção de cópias de segurança são suportadas para máquinas toostandard replicadas armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3d545-115">Up too72 hours of retention is supported for machines replicated toostandard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3d545-116">É criada automaticamente uma política de replicação para reativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="3d545-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="3d545-117">Em **Frequência de instantâneos consistentes com a aplicação**, especifique a frequência (em minutos) com que os pontos de recuperação que contêm os instantâneos consistentes com aplicações serão criados.</span><span class="sxs-lookup"><span data-stu-id="3d545-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="3d545-118">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d545-118">Click **OK**.</span></span> <span data-ttu-id="3d545-119">política de Olá deve ser criada na 30 segundos too60.</span><span class="sxs-lookup"><span data-stu-id="3d545-119">hello policy should be created in 30 too60 seconds.</span></span>

![Geração da política de replicação](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="3d545-121">Associe um servidor de configuração a uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="3d545-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="3d545-122">Escolha toowhich de política de replicação de Olá pretende que o servidor de configuração de Olá tooassociate.</span><span class="sxs-lookup"><span data-stu-id="3d545-122">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="3d545-123">Clique em **Associar**.</span><span class="sxs-lookup"><span data-stu-id="3d545-123">Click **Associate**.</span></span>
<span data-ttu-id="3d545-124">![Associar servidor de configuração](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="3d545-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="3d545-125">Selecione o servidor de configuração de Olá Olá lista de servidores.</span><span class="sxs-lookup"><span data-stu-id="3d545-125">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="3d545-126">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d545-126">Click **OK**.</span></span> <span data-ttu-id="3d545-127">servidor de configuração de Olá deve ser associada em um tootwo minutos.</span><span class="sxs-lookup"><span data-stu-id="3d545-127">hello configuration server should be associated in one tootwo minutes.</span></span>

![Associação do servidor de configuração](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="3d545-129">Editar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="3d545-129">Edit a replication policy</span></span>
1. <span data-ttu-id="3d545-130">Escolha a política de replicação de Olá para o qual pretende que as definições de replicação tooedit.</span><span class="sxs-lookup"><span data-stu-id="3d545-130">Choose hello replication policy for which you want tooedit replication settings.</span></span>
<span data-ttu-id="3d545-131">![Editar a política de replicação](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="3d545-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="3d545-132">Clique em **Editar Definições**.</span><span class="sxs-lookup"><span data-stu-id="3d545-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="3d545-133">![Editar definições da política de replicação](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="3d545-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="3d545-134">Alterar as definições de Olá com base na sua necessidade.</span><span class="sxs-lookup"><span data-stu-id="3d545-134">Change hello settings based on your need.</span></span>
4. <span data-ttu-id="3d545-135">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3d545-135">Click **Save**.</span></span> <span data-ttu-id="3d545-136">política de Olá deverá ser guardado em dois minutos toofive, consoante o número de VMs estiver a utilizar essa política de replicação.</span><span class="sxs-lookup"><span data-stu-id="3d545-136">hello policy should be saved in two toofive minutes, depending on how many VMs are using that replication policy.</span></span>

![Guardar política de replicação](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="3d545-138">Desassocie um servidor de configuração de uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="3d545-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="3d545-139">Escolha toowhich de política de replicação de Olá pretende que o servidor de configuração de Olá tooassociate.</span><span class="sxs-lookup"><span data-stu-id="3d545-139">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="3d545-140">Clique em **Desassociar**.</span><span class="sxs-lookup"><span data-stu-id="3d545-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="3d545-141">Selecione o servidor de configuração de Olá Olá lista de servidores.</span><span class="sxs-lookup"><span data-stu-id="3d545-141">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="3d545-142">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d545-142">Click **OK**.</span></span> <span data-ttu-id="3d545-143">servidor de configuração de Olá deve ser desassociada em um tootwo minutos.</span><span class="sxs-lookup"><span data-stu-id="3d545-143">hello configuration server should be dissociated in one tootwo minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3d545-144">Não é possível desassociar um servidor de configuração se existir pelo menos um item replicado através da política de Olá.</span><span class="sxs-lookup"><span data-stu-id="3d545-144">You cannot dissociate a configuration server if there is at least one replicated item using hello policy.</span></span> <span data-ttu-id="3d545-145">Certifique-se de que não foram encontrados itens replicados através da política de Olá antes de desassociar o servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="3d545-145">Make sure there are no replicated items using hello policy before you dissociate hello configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="3d545-146">Eliminar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="3d545-146">Delete a replication policy</span></span>

1. <span data-ttu-id="3d545-147">Escolha a política de replicação de Olá que pretende que o toodelete.</span><span class="sxs-lookup"><span data-stu-id="3d545-147">Choose hello replication policy that you want toodelete.</span></span>
2. <span data-ttu-id="3d545-148">Clique em **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="3d545-148">Click **Delete**.</span></span> <span data-ttu-id="3d545-149">política de Olá deve ser eliminada em 30 too60 segundos.</span><span class="sxs-lookup"><span data-stu-id="3d545-149">hello policy should be deleted in 30 too60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3d545-150">Não é possível eliminar uma política de replicação se tiver pelo menos um tooit de servidor associado à configuração.</span><span class="sxs-lookup"><span data-stu-id="3d545-150">You cannot delete a replication policy if it has at least one configuration server associated tooit.</span></span> <span data-ttu-id="3d545-151">Certifique-se de que não foram encontrados itens replicados utilizando a política de Olá e eliminar que todos os Olá associados a servidores de configuração antes de eliminar política Olá.</span><span class="sxs-lookup"><span data-stu-id="3d545-151">Make sure there are no replicated items using hello policy and delete all hello associated configuration servers before you delete hello policy.</span></span>
