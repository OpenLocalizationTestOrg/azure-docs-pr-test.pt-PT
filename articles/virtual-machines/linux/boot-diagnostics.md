---
title: "diagnóstico de aaaBoot para computadores virtuais Linux no Azure | Documentação da Microsoft"
description: "Descrição geral das funcionalidades depuração dois Olá para computadores virtuais Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a>Como toouse arranque diagnóstico tootroubleshoot máquinas de virtuais Linux no Azure

Está agora disponível o suporte de duas funcionalidades de depuração no Azure: Saída da Consola e Captura de Ecrã para o modelo de implementação das Máquinas Virtuais do Azure (Resource Manager). 

Quando o seus próprios tooAzure de imagem ou mesmo arrancar uma das imagens da plataforma de Olá, pode ser muitos motivos por que motivo uma Máquina Virtual obtém num Estado não arranque. Ativar estas funcionalidades tooeasily diagnosticar e recuperar máquinas virtuais de falhas de arranque.

Para máquinas de virtuais do Linux, pode visualizar facilmente resultado Olá o início de sessão de consola do Olá Portal:

![Portal do Azure](./media/boot-diagnostics/screenshot1.png)
 
No entanto, para o Windows e máquinas virtuais do Linux, Azure também permite toosee uma captura de ecrã de Olá VM de hipervisor Olá:

![Erro](./media/boot-diagnostics/screenshot2.png)

Estas duas funcionalidades são suportadas para Máquinas Virtuais do Azure em todas as regiões. Tenha em atenção, capturas de ecrã e de saída podem demorar até too10 minutos tooappear na sua conta de armazenamento.

## <a name="common-boot-errors"></a>Erros de arranque comuns

- [Problemas de sistema de ficheiros](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [Problemas de kernel](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [Erros FSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Ativar o diagnóstico numa máquina virtual nova
1. Quando criar uma nova máquina Virtual do Portal de pré-visualização de Olá, selecione Olá **do Azure Resource Manager** da lista pendente de modelo de implementação Olá:
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. Configure Olá monitorização opção tooselect Olá conta do storage onde pretende que tooplace estes ficheiros de diagnóstico.
 
    ![Criar VM](./media/boot-diagnostics/screenshot4.jpg)

3. Se estiver a implementar a partir de um modelo Azure Resource Manager, navegue até tooyour recurso de Máquina Virtual e de acréscimo secção de perfil de diagnóstico de Olá. Lembre-se o cabeçalho de versão de API do toouse Olá "2015-06-15".

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. perfil de diagnóstico de Olá permite-lhe conta do storage tooselect olá onde pretende tooput estes registos.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a>Atualizar uma máquina virtual existente

diagnóstico de arranque tooenable através do portal Olá, também pode atualizar uma máquina virtual existente através do portal Olá. Selecione Olá opção de diagnóstico de arranque e de guardar. Reinicie o efeito de tootake Olá VM.

![Atualizar VM Existente](./media/boot-diagnostics/screenshot5.png)