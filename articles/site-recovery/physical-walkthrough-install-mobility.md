---
title: "Olá aaaInstall serviço de mobilidade de replicação do servidor físico tooAzure | Microsoft Docs"
description: "Este artigo descreve como tooinstall Olá agente do serviço de mobilidade em servidores físicos a replicar tooAzure com o serviço do Azure Site Recovery Olá."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a>Passo 9: Instalar o serviço de mobilidade Olá


Este artigo descreve como componente de serviço de mobilidade do tooinstall Olá quando replicar no local tooAzure de servidores físicos Windows/Linux, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.

Olá serviço de mobilidade obtém dados, escreve numa máquina e reencaminha-os toohello servidor de processos. Deve ser instalado em cada servidor que pretende que o tooreplicate tooAzure.

Pode instalar o serviço de mobilidade Olá manualmente ou utilizar uma instalação de push de Olá recuperação de Site processar servidor quando a replicação está ativada ou utilizando uma ferramenta como o System Center Configuration Manager. Se utilizar a instalação push do serviço Olá está instalado no servidor de Olá ao ativar a replicação.

Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Instalar manualmente

1. Verifique Olá [pré-requisitos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para a instalação manual.
2. Siga [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para a instalação manual através do portal Olá.
3. Se preferir tooinstall Olá linha de comandos, siga [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Instalar a partir do servidor de processos de Olá

Se pretender toopush hello do servidor de processos de Olá a instalação do serviço de mobilidade quando ativar a replicação para uma máquina, precisa de uma conta que pode ser utilizada pela máquina do Olá processo servidor tooaccess Olá. conta de Olá só é utilizada para a instalação de push Olá.

1. Se ainda não criou uma conta, o que pretende utilizar estas diretrizes:

    - Pode utilizar um domínio ou conta local
    - Para o Windows, se não estiver a utilizar uma conta de domínio, terá de toodisable controlo de acesso de utilizador remoto no computador local Olá. toodo, Olá registar em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, adicionar a entrada de DWORD Olá **LocalAccountTokenFilterPolicy**, com um valor de 1.
    - Se pretender que entrada de registo de Olá tooadd para Windows de um CLI, escreva:

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - Para Linux conta Olá deve ser a raiz no servidor de Linux Olá origem.

2. Em seguida, siga [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se pretender que o serviço de mobilidade Olá toopush em VMs do Windows ou Linux em execução.

## <a name="other-installation-methods"></a>Outros métodos de instalação

- [Saiba mais sobre](site-recovery-install-mobility-service-using-sccm.md) instalar o serviço de mobilidade Olá utilizando o Configuration Manager
- [Saiba mais sobre](site-recovery-automate-mobility-service-install.md) instalação com o Automation DSC do Azure.


## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 10: Ativar a replicação](physical-walkthrough-enable-replication.md)
