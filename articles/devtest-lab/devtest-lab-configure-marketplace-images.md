---
title: "definições de imagens do Azure Marketplace aaaConfigure no Azure DevTest Labs | Microsoft Docs"
description: Configurar as imagens do Azure Marketplace podem ser utilizadas ao criar uma VM no Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a>Configurar definições de imagem do Azure Marketplace no Azure DevTest Labs
DevTest Labs suporta criar VMs baseadas nas imagens do Azure Marketplace, dependendo de como tiver configurado o Azure Marketplace imagens toobe utilizado no laboratório. Este artigo mostra como toospecify que, se existirem, as imagens do Azure Marketplace podem ser utilizado ao criar as VMs num laboratório. Isto garante que a sua equipa tiver apenas imagens do Marketplace toohello acesso que precisam. 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a>Selecione as imagens do Azure Marketplace são permitidas quando criar uma VM
1. Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de Olá.
3. Na lista de Olá de laboratórios, selecione laboratório pretendido Olá. 
4. No painel do laboratório de Olá, selecione **políticas de configuração e**.
5. Do laboratório **políticas de configuração e** painel em **Bases de máquinas virtuais**, selecione **imagens do Marketplace**.
6. Especifique se pretende que todos os Olá qualificado Azure Marketplace imagens toobe disponível para utilização como base de uma nova VM. Se selecionar **Sim**, em seguida, todos os Olá Azure Marketplace que cumpram Olá, todos os seguintes critérios são permitidas imagens na laboratório Olá:
   
   * imagem de Olá cria uma única VM, **e**
   * imagem de Olá utiliza VMs do Azure Resource Manager tooprovision, **e**
   * imagem de Olá não necessita de comprar um plano de licenciamento extra
     
    Se quiser não toobe imagens permitido, ou se quiser toospecify que imagens podem ser utilizados, selecione **não**.
     
     ![Opção tooallow todos os toobe de imagens do Marketplace utilizado como base imagens para VMs](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. Se selecionar **não** toohello anterior passo, hello **permitidos imagens/selecionar todos os** caixa de verificação está ativada. 
   Pode utilizar esta opção juntamente com Olá pesquisa caixa tooquickly selecione ou desmarque todas as Olá itens apresentados na lista de Olá.
   * Selecione as imagens do Azure Marketplace Olá pretende tooallow para a criação de VM individualmente marcando a caixa de verificação correspondente de cada imagem.
   * Selecione nada Olá lista se não quiser tooallow qualquer toobe de imagens do Azure Marketplace utilizado no laboratório Olá.
   
    ![Pode especificar as imagens do Azure Marketplace podem ser utilizadas como base imagens para VMs](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Passos seguintes
Assim que tiver configurado como imagens do Azure Marketplace são permitidas quando criar uma VM, o passo seguinte Olá é demasiado[adicionar um laboratório de tooyour VM](devtest-lab-add-vm-with-artifacts.md).

