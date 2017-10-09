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
# <a name="manage-replication-policy-for-vmware-tooazure"></a>Gerir a política de replicação para tooAzure de VMware


## <a name="create-a-replication-policy"></a>Criar uma política de replicação

1. Selecione **Gerir** > **Infraestrutura do Site Recovery**.
2. Selecione **Políticas de replicação** em **Para VMware e Máquinas físicas**.
3. Selecione **+Política de replicação**.

    ![Criar política de replicação](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. Introduza o nome da política Olá.

5. No **limiar RPO**, especificar Olá RPO limite. Serão gerados alertas quando a replicação contínua exceder este limite.
6. No **retenção do ponto de recuperação**, especifique (em horas) Olá duração da janela de retenção de Olá para cada ponto de recuperação. Máquinas protegidas podem ser recuperados tooany ponto dentro de uma janela de retenção.

    > [!NOTE]
    > Horas de too24 de retenção de cópias de segurança são suportadas para máquinas toopremium replicadas armazenamento. Horas de too72 de retenção de cópias de segurança são suportadas para máquinas toostandard replicadas armazenamento.

    > [!NOTE]
    > É criada automaticamente uma política de replicação para reativação pós-falha.

7. Em **Frequência de instantâneos consistentes com a aplicação**, especifique a frequência (em minutos) com que os pontos de recuperação que contêm os instantâneos consistentes com aplicações serão criados.

8. Clique em **OK**. política de Olá deve ser criada na 30 segundos too60.

![Geração da política de replicação](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a>Associe um servidor de configuração a uma política de replicação
1. Escolha toowhich de política de replicação de Olá pretende que o servidor de configuração de Olá tooassociate.
2. Clique em **Associar**.
![Associar servidor de configuração](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)

3. Selecione o servidor de configuração de Olá Olá lista de servidores.
4. Clique em **OK**. servidor de configuração de Olá deve ser associada em um tootwo minutos.

![Associação do servidor de configuração](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a>Editar uma política de replicação
1. Escolha a política de replicação de Olá para o qual pretende que as definições de replicação tooedit.
![Editar a política de replicação](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)

2. Clique em **Editar Definições**.
![Editar definições da política de replicação](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)

3. Alterar as definições de Olá com base na sua necessidade.
4. Clique em **Guardar**. política de Olá deverá ser guardado em dois minutos toofive, consoante o número de VMs estiver a utilizar essa política de replicação.

![Guardar política de replicação](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a>Desassocie um servidor de configuração de uma política de replicação
1. Escolha toowhich de política de replicação de Olá pretende que o servidor de configuração de Olá tooassociate.
2. Clique em **Desassociar**.
3. Selecione o servidor de configuração de Olá Olá lista de servidores.
4. Clique em **OK**. servidor de configuração de Olá deve ser desassociada em um tootwo minutos.

    > [!NOTE]
    > Não é possível desassociar um servidor de configuração se existir pelo menos um item replicado através da política de Olá. Certifique-se de que não foram encontrados itens replicados através da política de Olá antes de desassociar o servidor de configuração de Olá.

## <a name="delete-a-replication-policy"></a>Eliminar uma política de replicação

1. Escolha a política de replicação de Olá que pretende que o toodelete.
2. Clique em **Eliminar**. política de Olá deve ser eliminada em 30 too60 segundos.

    > [!NOTE]
    > Não é possível eliminar uma política de replicação se tiver pelo menos um tooit de servidor associado à configuração. Certifique-se de que não foram encontrados itens replicados utilizando a política de Olá e eliminar que todos os Olá associados a servidores de configuração antes de eliminar política Olá.
