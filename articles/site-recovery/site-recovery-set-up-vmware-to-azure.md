---
title: "Configurar o ambiente de origem Olá (VMware tooAzure) | Microsoft Docs"
description: "Este artigo descreve como tooset cópias de segurança sua toostart de ambiente no local VMware virtual a replicar máquinas tooAzure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a>Configurar o ambiente de origem Olá (VMware tooAzure)
> [!div class="op_single_selector"]
> * [TooAzure de VMware](./site-recovery-set-up-vmware-to-azure.md)
> * [TooAzure físico](./site-recovery-set-up-physical-to-azure.md)

Este artigo descreve como tooset cópias de segurança sua toostart de ambiente no local virtual a replicar máquinas em execução no VMware tooAzure.

## <a name="prerequisites"></a>Pré-requisitos

artigo de Olá pressupõe que já criou:
- Um cofre dos serviços de recuperação no Olá [portal do Azure](http://portal.azure.com "portal do Azure").
- Uma conta dedicada o VMware vcenter que podem ser utilizadas para [a deteção automática](./site-recovery-vmware-to-azure.md).
- Uma máquina virtual no servidor de configuração que tooinstall Olá.

## <a name="configuration-server-minimum-requirements"></a>Requisitos mínimos do servidor de configuração
software de servidor de configuração de Olá deve ser implementado numa máquina virtual VMware altamente disponível. Olá, a tabela seguinte lista Olá mínimos de hardware, software e requisitos de rede para um servidor de configuração.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> Servidores proxy baseado em HTTPS não são suportadas pelo servidor de configuração de Olá.

## <a name="choose-your-protection-goals"></a>Escolha os seus objetivos de proteção

1. Olá portal do Azure, aceda toohello **dos serviços de recuperação** painel do cofre e selecione o cofre.
2. No menu de recursos de Olá do Cofre de Olá, aceda demasiado**introdução** > **recuperação de Site** > **passo 1: preparar a infraestrutura**  >  **Objetivo de proteção**.

    ![Selecione os objetivos](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. No **objetivo de proteção**, selecione **tooAzure**e escolha **Sim, com o VMware vSphere hipervisor**. Em seguida, clique em **OK**.

    ![Selecione os objetivos](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá
Configurar o ambiente de origem Olá envolve dois principais atividades:

- Instalar e registar um servidor de configuração com a recuperação de Site.
- Detete máquinas virtuais no local através da ligação de recuperação de Site tooyour local no VMware vCenter ou vSphere EXSi anfitriões.

### <a name="step-1-install-and-register-a-configuration-server"></a>Passo 1: Instalar e registar um servidor de configuração

1. Clique em **passo 1: preparar infraestrutura** > **origem**. No **preparar a origem**, se não tiver um servidor de configuração, clique em **+ o servidor de configuração** tooadd um.

    ![Configurar a origem](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. No Olá **Adicionar servidor** painel, verifique se **servidor de configuração** aparece no **tipo de servidor**.
4. Transfira o ficheiro de instalação do programa de configuração do Site Recovery Unified Olá.
5. Transferir a chave de registo do cofre Olá. Terá de chave de registo Olá quando executar a configuração do Unified. chave de Olá é válido durante cinco dias depois de gerá-la.

    ![Configurar a origem](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. Na máquina de Olá estiver a utilizar como servidor de configuração de Olá, execute **configuração de unificada do Azure Site Recovery** servidor de configuração do tooinstall Olá, o servidor de processos de Olá e o mestre de Olá servidor de destino.

#### <a name="run-azure-site-recovery-unified-setup"></a>Configuração de unificada de execução do Azure Site Recovery

> [!TIP]
> Registo do servidor de configuração falha se o tempo de Olá no relógio do sistema do computador é diferente da hora local em mais de cinco minutos. Sincronizar o relógio do seu sistema com um [hora Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar a instalação de Olá.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> servidor de configuração de Olá pode ser instalada através de linha de comandos. Para obter mais informações, consulte [instalar servidor de configuração de Olá utilizando as ferramentas da linha de comandos](http://aka.ms/installconfigsrv).

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a>Adicionar a conta de VMware Olá para a deteção automática

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a>Passo 2: Adicionar um vCenter
tooallow do Azure Site Recovery toodiscover máquinas virtuais em execução no seu ambiente no local, terá de tooconnect o servidor vCenter VMware ou vSphere ESXi anfitriões com a recuperação de Site.

Selecione **+ vCenter** toostart ligar um servidor VMware vCenter ou um anfitrião do VMware vSphere ESXi.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a>Problemas comuns
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Passos seguintes
[Configurar o ambiente de destino](./site-recovery-prepare-target-vmware-to-azure.md) no Azure.
