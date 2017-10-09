---
title: "FAQ do Cofre de serviços de aaaRecovery | Microsoft Docs"
description: "Esta versão do Olá FAQ suporta a versão de pré-visualização pública Olá do Olá serviço de cópia de segurança do Azure. Respostas toofrequently mais frequentes sobre o sobre o agente de cópia de segurança de Olá, cópia de segurança e retenção, recuperação, segurança e outras perguntas comuns sobre Olá solução de cópia de segurança do Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "solução de cópia de segurança; serviço de cópia de segurança"
ms.assetid: 5f55b500-1ee9-4f64-9306-02d6f7a8eded
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/21/2016
ms.author: markgal;trinadhk;
ms.openlocfilehash: 882b2e67ed424dc9f3681a8870e6b4c7b4cdcaec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vault---faq"></a>Cofre dos Serviços de Recuperação – FAQ
Este artigo fornece o Cofre de serviços de informações específicas tooRecovery e complementa Olá [FAQ de cópia de segurança do Azure](backup-azure-backup-faq.md). Olá FAQ de cópia de segurança do Azure fornece o conjunto completo de Olá de perguntas e respostas sobre Olá serviço de cópia de segurança do Azure.  

Pode colocar perguntas sobre o Backup do Azure no Olá secção Disqus deste artigo ou um artigo relacionado. Também pode publicar perguntas sobre Olá serviço de cópia de segurança do Azure no Olá [fórum de discussão](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Os cofres dos Serviços de Recuperação baseiam-se no Resource Manager. Os cofres do Backup (modo clássico) ainda são suportados? <br/>
Sim, os cofres da Cópia de Segurança ainda são suportados. Crie cofres de cópia de segurança no Olá [portal clássico](https://manage.windowsazure.com). Crie cofres dos serviços de recuperação no Olá [portal do Azure](https://portal.azure.com). No entanto Recomendamos vivamente toocreate recuperação cofre dos serviços de que todos os melhoramentos futuros estará disponível apenas no Cofre de serviços de recuperação.

## <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Pode migrar um cofre de serviços de recuperação de tooa de Cofre de cópia de segurança? <br/>
Infelizmente não, neste momento, não é possível migrar conteúdo Olá um tooa do Cofre de cópia de segurança que do cofre dos serviços de recuperação. Estamos a tentar adicionar esta funcionalidade, mas não está disponível como parte da Pré-visualização Pública.

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Os cofres dos Serviços de Recuperação suportam VMs clássicas ou VMs no Resource Manager? <br/>
Os cofres dos Serviços de Recuperação suportam ambos os modelos.  Pode efetuar cópias de segurança de uma VM criada no portal clássico do Olá (que são das VMs no modo clássico) ou uma VM criada no Olá portal do Azure (que são baseado no Gestor de recursos) dos serviços de recuperação tooa do cofre.

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-toomigrate-my-vms-from-classic-mode-tooresource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a>Efetuei cópia de segurança das minhas VMs clássicas no cofre de cópia de segurança. Agora pretendo toomigrate minhas VMs do modo de Gestor de tooResource modo clássico.  Como posso efetuar uma cópia de segurança das mesmas no cofre dos serviços de recuperação?
Cópias de segurança de VMs clássicas no Cofre de cópia de segurança não migrar automaticamente toorecovery Cofre de serviços quando migra Olá VMs do clássico tooResource modo Manager. Siga estes passos para migrar as cópias de segurança de VMs:

1. No Cofre de cópia de segurança, aceda demasiado**itens protegidos** separador e selecione Olá VM. Clique em [Parar Proteção](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Deixe a opção *Eliminar dados de cópia de segurança associados* **desmarcada**.
2. No Olá [portal do Azure](https://portal.azure.com), aceda a toohello **extensões** menu para Olá VM e desinstalar Olá **VMSnapshot/VMSnapshotLinux** extensão.
3. Migre máquina virtual de Olá do modo de Gestor de tooResource modo clássico. Certifique-se de que o armazenamento e de rede correspondente toovirtual máquina também são migrados tooResource Manager modo.
4. Criar um cofre dos serviços de recuperação e configurar a cópia de segurança Olá migrar máquina virtual a utilizar **cópia de segurança** ação por cima do dashboard do cofre. Saiba mais sobre como demasiado[ativar cópia de segurança no Cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md)
