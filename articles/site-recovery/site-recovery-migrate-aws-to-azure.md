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
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a>Migrar máquinas virtuais no tooAzure Amazon Web Services (AWS) com o Azure Site Recovery

Este artigo descreve como toomigrate Windows em AWS instâncias máquinas de virtuais tooAzure com Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.

Migração de forma eficaz é uma ativação pós-falha do AWS tooAzure. Não é possível tooAWS de máquinas de reativação pós-falha, e não existe nenhuma replicação em curso. Este artigo descreve Olá passos de migração no Olá portal do Azure e baseiam-se as instruções de Olá para [replicar um tooAzure de máquina física](site-recovery-vmware-to-azure.md).

Publique comentários ou perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

## <a name="supported-operating-systems"></a>Sistemas operativos suportados

Recuperação de sites pode ser instâncias utilizado toomigrate EC2 com qualquer uma das Olá os seguintes sistemas operativos:

- Windows (apenas 64 bits)
    - Windows Server 2008 R2 SP1 + (controladores do Citrix PV ou apenas os controladores de AWS PV. **As instâncias em execução controladores de VM de RedHat PV não são suportadas**) Windows Server 2012 Windows Server 2012 R2
- Linux (apenas 64 bits)
    - Red Hat Enterprise Linux 6.7 (apenas para instâncias HVM virtualizada)

## <a name="prerequisites"></a>Pré-requisitos

Eis o que precisa para esta implementação:

* **Servidor de configuração**: um Amazon EC2 implementação da VM com o Windows Server 2012 R2 como servidor de configuração de Olá. Por predefinição, hello outros componentes do Azure Site Recovery (servidor de processos e o servidor de destino principal) são instalados quando implementar o servidor de configuração de Olá. Este artigo descreve Olá passos de migração no Olá portal do Azure e baseiam-se as instruções de Olá para [Saiba mais](site-recovery-components.md)

* **Instâncias de EC2**: Olá Amazon EC2 instâncias de máquinas virtuais que pretende que o toomigrate.

## <a name="deployment-steps"></a>Passos da implementação

1. Crie um cofre dos Serviços de Recuperação.
2. Olá, grupo de segurança das suas instâncias EC2 deve ter regras configuradas tooallow comunicação entre a instância de EC2 Olá que pretende que o toomigrate e instância Olá no qual planeia toodeploy Olá servidor de configuração.

3. No Olá mesmo Amazon Virtual nuvem privada como as instâncias de EC2, implementar um servidor de configuração de ASR. Consulte Olá VMware / físico tooAzure pré-requisitos de requisitos de implementação do servidor de configuração.

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  Depois do servidor de configuração é implementado no AWS e registado com o Cofre dos serviços de recuperação, deverá ver o servidor de configuração de Olá e servidor de processos em infraestrutura de recuperação de sites como mostrado abaixo:

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. Após implementar o servidor de configuração de Olá (poderá demorar até too15 minustes para o mesmo tooappear), validar que este consegue comunicar com Olá VMs que pretende que o toomigrate.

6. [Configurar as definições de replicação](site-recovery-setup-replication-settings-vmware.md).

7. Ativar a replicação: Ativar a replicação para Olá VMs que pretende toomigrate. Pode detetar instâncias de EC2 Olá utilizando endereços IP privados Olá, que pode obter a partir da consola de EC2 Olá.

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. Depois de instâncias de Olá EC2 tenham sido protegidas e Olá replicação tooAzure estiver concluída, [executar uma ativação pós-falha de teste](site-recovery-test-failover-to-azure.md) toovalidate desempenho da sua aplicação no Azure.

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. Execute uma ativação pós-falha do AWS tooAzure para cada VM. Opcionalmente, pode criar um plano de recuperação e executar uma ativação pós-falha, toomigrate várias máquinas virtuais do AWS tooAzure. [Saiba mais](site-recovery-create-recovery-plans.md) sobre os planos de recuperação.

10. Para a migração, não precisa de toocommit uma ativação pós-falha. Em vez disso, selecione a opção de concluir a migração de Olá para cada máquina que pretende toomigrate. Olá ação de concluir a migração conclusão do processo de migração de Olá, remove a replicação da máquina de Olá e deixa de recuperação de sites para a máquina Olá de faturação.

    ![Migrar](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a>Passos seguintes

- [Preparar máquinas migradas tooenable replicação](site-recovery-azure-to-azure-after-migration.md) tooanother região para as necessidades de recuperação após desastre.
- Comece a proteger as suas cargas de trabalho ao [replicar máquinas virtuais do Azure.](site-recovery-azure-to-azure.md)
