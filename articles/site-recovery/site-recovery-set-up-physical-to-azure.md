---
title: "Configurar o ambiente de origem Olá (servidores físicos tooAzure) | Microsoft Docs"
description: "Este artigo descreve como tooset cópias de segurança sua toostart de ambiente no local replicar servidores físicos que executem Windows ou Linux no Azure."
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a>Configurar o ambiente de origem Olá (servidor físico tooAzure)
> [!div class="op_single_selector"]
> * [TooAzure de VMware](./site-recovery-set-up-vmware-to-azure.md)
> * [TooAzure físico](./site-recovery-set-up-physical-to-azure.md)

Este artigo descreve como tooset cópias de segurança sua toostart de ambiente no local replicar servidores físicos que executem Windows ou Linux no Azure.

## <a name="prerequisites"></a>Pré-requisitos

artigo de Olá pressupõe que já tem:
1. Um cofre dos serviços de recuperação Olá [portal do Azure](http://portal.azure.com "portal do Azure").
3. Um computador físico no servidor de configuração que tooinstall Olá.

### <a name="configuration-server-minimum-requirements"></a>Requisitos mínimos do servidor de configuração
Olá, a tabela seguinte lista Olá mínimos de hardware, software e requisitos de rede para um servidor de configuração.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> Servidores proxy baseado em HTTPS não são suportadas pelo servidor de configuração de Olá.

## <a name="choose-your-protection-goals"></a>Escolha os seus objetivos de proteção

1. Olá portal do Azure, aceda toohello **dos serviços de recuperação** cofres dos painel e selecione o cofre.
2. No Olá **recursos** menu do Cofre de Olá, clique em **introdução** > **recuperação de Site** > **passo 1: preparar Infraestrutura** > **objetivo de proteção**.

    ![Selecione os objetivos](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. No **objetivo de proteção**, selecione **tooAzure** e **não virtualizados/outras**e, em seguida, clique em **OK**.

    ![Selecione os objetivos](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

1. No **preparar a origem**, se não tiver um servidor de configuração, clique em **+ o servidor de configuração** tooadd um.

  ![Configurar a origem](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. No Olá **Adicionar servidor** painel, verifique se **servidor de configuração** aparece no **tipo de servidor**.
4. Transfira o ficheiro de instalação do programa de configuração do Site Recovery Unified Olá.
5. Transferir a chave de registo do cofre Olá. Terá de chave de registo Olá quando executar a configuração do Unified. chave de Olá é válido durante cinco dias depois de gerá-la.

    ![Configurar a origem](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. Na máquina de Olá estiver a utilizar como servidor de configuração de Olá, execute **configuração de unificada do Azure Site Recovery** servidor de configuração do tooinstall Olá, o servidor de processos de Olá e o mestre de Olá servidor de destino.

#### <a name="run-azure-site-recovery-unified-setup"></a>Configuração de unificada de execução do Azure Site Recovery

> [!TIP]
> Registo do servidor de configuração falha se o tempo de Olá no relógio do sistema do computador é mais de cinco minutos retire hora local. Sincronizar o relógio do seu sistema com um [hora server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar a instalação de Olá.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> servidor de configuração de Olá pode ser instalada através de uma linha de comandos. Para obter mais informações, consulte [instalar servidor de configuração com as ferramentas da linha de comandos](http://aka.ms/installconfigsrv).


## <a name="common-issues"></a>Problemas comuns

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Passos seguintes

Passo seguinte envolve [como configurar o ambiente de destino](./site-recovery-prepare-target-physical-to-azure.md) no Azure.
