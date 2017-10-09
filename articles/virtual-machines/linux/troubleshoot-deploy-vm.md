---
title: "aaaTroubleshoot implementar problemas da máquina virtual com Linux no Azure | Microsoft Docs"
description: "Resolva problemas da máquina virtual Linux implementação no modelo de implementação Azurethe Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a>Resolver problemas de máquina virtual Linux implementar no Azure

problemas de implementação de máquina virtual (VM) tootroubleshoot no Azure, reveja Olá [principais problemas](#top-issues) para falhas e resoluções comuns.

Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no [Olá fóruns do MSDN Azure e Stack Overflow](https://azure.microsoft.com/support/forums/). Em alternativa, pode ficheiro um incidente de suporte do Azure. Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporta**.

## <a name="top-issues"></a>Problemas principais
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a>Não é possível suportar cluster Olá Olá solicitado o tamanho da VM
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Repita o pedido de Olá utilizando um tamanho mais pequeno da VM.
- Se hello o tamanho do Olá pedido que não é possível alterar a VM:
    - Pare todas as VMs de Olá no conjunto de disponibilidade de Olá. Clique em **grupos de recursos** > o grupo de recursos > **recursos** > o conjunto de disponibilidade > **máquinas virtuais** > sua máquina virtual >  **Parar**.
    - Após todos os Olá parar de VMs, criar Olá VM tamanho Olá assim o desejar.
    - Iniciar Olá nova VM primeiro e, em seguida, selecione cada Olá parado VMs e clique em Iniciar.


## <a name="hello-cluster-does-not-have-free-resources"></a>Olá cluster não tem recursos gratuitos
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Repita o pedido de Olá mais tarde.
- Se hello nova VM pode ser faz parte de uma disponibilidade diferente conjunto
    - Criar uma VM de um conjunto de disponibilidade diferente (no Olá mesma região).
    - Adicionar Olá nova VM toohello mesma rede virtual.

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Como ativar o meu crédito mensal para Visual studio Enterprise (BizSpark)

tooactivate sua mensal de crédito, consulte este [artigo](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a>Por que motivo devo instalar não Olá GPU controlador para uma VM de NV Ubuntu?

Atualmente, o suporte de Linux GPU só está disponível em VMs do Azure NC Ubuntu Server 16.04 LTS a executar. Para obter mais informações, consulte [configurar controladores GPU para VMs de série N executar Linux](n-series-driver-setup.md).

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a>A minha controladores estão em falta para a minha VM do Linux série N

Controladores para as VMs baseadas em Linux estão localizadas [aqui](n-series-driver-setup.md). 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>Não é possível localizar a uma instância GPU na minha VM série N

tootake partido das capacidades GPU Olá das VMs do Azure de N série com o Windows Server 2016 ou o Windows Server 2012 R2, tem de instalar os controladores da placa NVIDIA em cada VM após a implementação. As informações de configuração de controladores estão disponíveis para [VMs do Windows](../windows/n-series-driver-setup.md) e [VMs com Linux](n-series-driver-setup.md).

## <a name="is-n-series-vms-available-in-my-region"></a>Série N VMs está disponível na minha região?

Pode verificar a disponibilidade de Olá de Olá [produtos disponíveis por tabela de região](https://azure.microsoft.com/regions/services)e preços [aqui](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>Não sou consegue toosee família de tamanho da VM que pretendo quando redimensionar a minha VM.

Quando uma VM está em execução, é implementado tooa servidor físico. servidores físicos do Olá em regiões do Azure estão agrupados em clusters de hardware físico comum. Redimensionar uma VM que necessita de clusters de hardware do Olá VM toobe movido toodifferent é diferente consoante o modelo de implementação foi utilizado toodeploy Olá VM.

- VMs implementadas no modelo de implementação clássica, implementação de serviço de nuvem Olá tem de ser removidas e a implementar toochange Olá VMs tooa tamanho outra família de tamanho.

- VMs implementadas no modelo de implementação do Resource Manager, tem de parar todas as VMs no conjunto antes de alterar o tamanho de Olá qualquer VM no conjunto de disponibilidade de Olá de disponibilidade de Olá.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Olá listado tamanho da VM não é suportado durante a implementação num conjunto de disponibilidade.

Escolha um tamanho que é suportado no cluster de conjunto de disponibilidade a Olá. Recomenda-se ao criar que um conjunto de disponibilidade toochoose Olá maior tamanho da VM pensa que precisa e tem que ser a primeira toohello de implementação que do conjunto de disponibilidade.

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a>Quais as distribuições de Linux/as versões são suportadas no Azure?

Pode encontrar a lista de Olá em Linux no [Azure-Endorsed distribuições](endorsed-distros.md).

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>Pode adicionar um conjunto de disponibilidade de tooan VMS clássicas existente?

Sim. Pode adicionar um existente clássico VM tooa novo ou existente do conjunto de disponibilidade. Para obter mais informações consulte [adicionar um conjunto de disponibilidade de tooan de máquina virtual existente](../windows/classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Passos seguintes
Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no [Olá fóruns do MSDN Azure e Stack Overflow](https://azure.microsoft.com/support/forums/).

Em alternativa, pode ficheiro um incidente de suporte do Azure. Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporta**.
