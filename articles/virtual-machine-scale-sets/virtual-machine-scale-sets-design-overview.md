---
title: "aaaDesign considerações para conjuntos de dimensionamento de Máquina Virtual do Azure | Microsoft Docs"
description: "Saiba mais sobre as considerações de design para os conjuntos de dimensionamento de Máquina Virtual do Azure"
keywords: "conjuntos de dimensionamento de máquina virtual de máquina virtual do Linux,"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: c27c6a59-a0ab-4117-a01b-42b049464ca1
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: f8644d36fe5903bd4b74df26dca5dc3211ee3516
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="design-considerations-for-scale-sets"></a>Considerações de design para conjuntos de dimensionamento
Este tópico descreve considerações de design para conjuntos de dimensionamento de Máquina Virtual. Para obter informações sobre quais são os conjuntos de dimensionamento de Máquina Virtual, consulte demasiado[descrição geral de conjuntos de dimensionamento de Máquina Virtual](virtual-machine-scale-sets-overview.md).

## <a name="when-toouse-scale-sets-instead-of-virtual-machines"></a>Quando toouse conjuntos de dimensionamento em vez de máquinas virtuais?
Geralmente, conjuntos de dimensionamento são úteis para implementar a infraestrutura de elevada disponibilidade em que um conjunto de máquinas têm configuração semelhante. No entanto, algumas funcionalidades só estão disponíveis nos conjuntos de dimensionamento enquanto outras funcionalidades só estão disponíveis nas VMs. Na ordem toomake uma decisão informada sobre quando toouse cada tecnologia, iremos deve primeiro Observe algumas das funcionalidades de Olá utilizada frequentemente que estão disponíveis em conjuntos de dimensionamento, mas não VMs:

### <a name="scale-set-specific-features"></a>Funcionalidades de específicas do conjunto de dimensionamento

- Depois de especificar a configuração de conjunto de dimensionamento de Olá, pode simplesmente atualizar Olá "capacidade" propriedade toodeploy mais VMs em paralelo. Isto é muito mais simples do que escrever um tooorchestrate script implementar várias VMs individuais em paralelo.
- Pode [um conjunto de dimensionamento de escala de utilização do Azure de dimensionamento automático tooautomatically](./virtual-machine-scale-sets-autoscale-overview.md) mas VMs não individuais.
- Pode [VMs de conjunto de dimensionamento de recriação de imagem](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-a-vm) mas [VMs individuais não](https://docs.microsoft.com/rest/api/compute/virtualmachines).
- Pode [bandeira](./virtual-machine-scale-sets-design-overview.md) conjunto de dimensionamento de VMs para uma maior fiabilidade e tempos de implementação mais rápidos. Não é possível fazê-com VMs individuais, a menos que escrever código personalizado toodo isto.
- Pode especificar um [atualizar política](./virtual-machine-scale-sets-upgrade-scale-set.md) toomake-tooroll fácil saída atualizações entre VMs no seu conjunto de dimensionamento. Com VMs individuais, é necessário orquestrar atualizações por si.

### <a name="vm-specific-features"></a>Funcionalidades específicas do VM

No Olá por outro lado, algumas funcionalidades só estão disponíveis em VMs (pelo menos para a hora de Olá):

- Pode anexar toospecific de discos de dados VMs individuais, mas os dados anexados discos estão configurados para todas as VMs num conjunto de dimensionamento.
- Pode anexar tooindividual de discos de dados não vazios VMs, mas não as VMs num conjunto de dimensionamento.
- Pode instantâneos de uma VM individual, mas não uma VM num conjunto de dimensionamento.
- Pode capturar uma imagem de uma VM individual, mas não a partir de uma VM num conjunto de dimensionamento.
- Pode migrar uma VM individual de discos de toomanaged nativo de discos, mas não o conseguir fazer para as VMs num conjunto de dimensionamento.
- Pode atribuir endereços IP públicos do IPv6 tooindividual VM nics mas não é possível fazer para as VMs num conjunto de dimensionamento. Tenha em atenção que pode atribuir endereços IP públicos do IPv6 balanceadores tooload à frente de qualquer uma das VMs individuais ou conjunto de dimensionamento de VMs.

## <a name="storage"></a>Armazenamento

### <a name="scale-sets-with-azure-managed-disks"></a>Conjuntos de dimensionamento com discos gerida do Azure
Podem ser criados conjuntos de dimensionamento com [Azure geridos discos](../virtual-machines/windows/managed-disks-overview.md) em vez de contas do storage do Azure tradicional. Os discos geridos fornecem Olá seguintes vantagens:
- Não dispõe de toopre-criar um conjunto de contas do storage do Azure para as VMs de conjunto de dimensionamento de Olá.
- Pode definir [discos de dados ligados](virtual-machine-scale-sets-attached-disks.md) para Olá VMs no seu dimensionamento definido.
- Conjuntos de dimensionamento podem ser configurados demasiado[suporta se too1, 000 VMs num conjunto](virtual-machine-scale-sets-placement-groups.md). 

Se tiver um modelo existente, também pode [atualizar Olá modelo toouse discos geridos](virtual-machine-scale-sets-convert-template-to-md.md).

### <a name="user-managed-storage"></a>Armazenamento gerida pelo utilizador
Um conjunto de dimensionamento não está definido com discos gerida do Azure baseia-se nos discos SO Olá de toostore de contas de armazenamento criados pelo utilizador de Olá VMs no conjunto de Olá. Um rácio de 20 VMs por conta de armazenamento ou menos recomenda tooachieve máximo e/s bem como tirar partido das _provocam um aprovisionamento_ (ver abaixo). Também é recomendável que distribuídos carateres de início de Olá dos nomes de conta de armazenamento Olá por Olá por letras do alfabeto. Se o fizer, ajuda a propagar-se a carga em sistemas diferentes de internos. 


## <a name="overprovisioning"></a>Provocam um aprovisionamento
Conjuntos de dimensionamento atualmente predefinido demasiado "provocam um aprovisionamento" VMs. Com provocam um aprovisionamento de ativada, escala Olá defina realmente spins mais VMS que pediu, em seguida, elimina Olá VMs Extras assim que o número de VMs de pedido de Olá são aprovisionadas com êxito. Provocam um aprovisionamento melhora aprovisionamento taxas de êxito e reduz o tempo de implementação. Não são cobradas para hello VMs Extras e não é considerado os limites de quota.

Enquanto provocam um aprovisionamento melhorar as taxas de êxito de aprovisionamento, pode causar confuso comportamento para uma aplicação que é não concebida toohandle VMs Extras apresentação e, em seguida, disappearing. tooturn provocam um aprovisionamento desligada, certifique-se de que tem Olá seguir cadeia no modelo: `"overprovision": "false"`. Podem encontrar mais detalhes no Olá [documentação da API de REST de conjunto de dimensionamento](/rest/api/virtualmachinescalesets/create-or-update-a-set).

Se o conjunto de dimensionamento utiliza armazenamento gerida pelo utilizador, e desativar provocam um aprovisionamento, pode ter mais de 20 VMs por conta de armazenamento, mas não se recomenda toogo acima 40 por motivos de desempenho de e/s. 

## <a name="limits"></a>Limites
Um conjunto de dimensionamento incorporado numa imagem do Marketplace (também conhecido como uma imagem de plataforma) e configurado toouse que discos gerida do Azure suporta uma capacidade de cópia de segurança too1, 000 VMs. Se configurar o seu toosupport de conjunto de dimensionamento mais do que 100 VMs, nem todos os cenários trabalho Olá mesmo (por exemplo o balanceamento de carga). Para obter mais informações, consulte [trabalhar com conjuntos de dimensionamento de máquina virtual grande](virtual-machine-scale-sets-placement-groups.md). 

Um conjunto configurado com as contas de armazenamento gerida pelo utilizador de dimensionamento é limitado too100 VMs (e 5 contas do storage são recomendadas para desta escala).

Um conjunto de dimensionamento incorporado numa imagem personalizada (um criadas por si) pode ter uma capacidade de segurança de VMs too100 quando configurado com discos gerida do Azure. Se o conjunto de dimensionamento de Olá está configurado com as contas de armazenamento gerida pelo utilizador, tem de criar todos os VHDs de disco de SO dentro de uma conta de armazenamento. Como resultado, máximo Olá recomendado número de VMs num conjunto de dimensionamento incorporado numa imagem personalizada e armazenamento gerida pelo utilizador é 20. Se desativar provocam um aprovisionamento, pode aceder a cópia de segurança too40.

Para obter mais VMs que estes limites permitem, terá de toodeploy conjuntos de dimensionamento vários conforme mostrado no [este modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/301-custom-images-at-scale).

