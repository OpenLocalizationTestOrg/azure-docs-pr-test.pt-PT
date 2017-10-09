---
title: "aaaCreate um laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Criar um laboratório no Azure DevTest Labs para máquinas virtuais"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Criar um laboratório no Azure DevTest Labs
Um laboratório no Azure DevTest Labs é infraestrutura Olá que abrange a um grupo de recursos, tais como máquinas virtuais (VMs), que lhe permite um melhor gerir esses recursos, especificando os limites e quotas. Este artigo explica Olá processo de criação de um laboratório utilizando Olá portal do Azure.

## <a name="prerequisites"></a>Pré-requisitos
toocreate um laboratório, tem de:

* Uma subscrição do Azure. toolearn sobre as opções de compra do Azure, consulte [como toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) ou [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). Tem de ser o proprietário de Olá de laboratório do Olá subscrição toocreate Olá.

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a>Passos toocreate um laboratório no Azure DevTest Labs
Olá, os passos seguintes mostram como toouse Olá toocreate portal do Azure um laboratório no DevTest Labs do Azure. 

1. Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. No menu principal Olá, no lado esquerdo Olá, selecione **mais serviços** (na Olá parte inferior da lista de Olá).

    ![Opção de menu Mais serviços](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. Na lista de serviços disponíveis, Olá **DevTest Labs**.
1. No Olá **DevTest Labs** painel, selecione **adicionar**.
   
    ![Adicionar um laboratório](./media/devtest-lab-create-lab/add-lab-button.png)

1. No Olá **criar um DevTest Lab** painel:
   
    1. Introduza um **nome do laboratório** para laboratório Olá de novo.
    2. Selecione Olá **subscrição** tooassociate com laboratório Olá.
    3. Selecione um **localização** no laboratório de Olá que toostore.
    4. Selecione **encerramento automático** toospecify se pretende tooenable - e definir os parâmetros de Olá-Olá automático a ser encerrado de VMs do laboratório Olá todas as. Olá funcionalidade de encerramento automático é essencialmente uma funcionalidade de custo guardar na qual pode especificar quando pretende Olá VM tooautomatically ser encerrado. Pode alterar as definições de encerramento automático depois de criar o laboratório de Olá seguindo os passos de Olá descritos no artigo Olá, [gerir todas as políticas para um laboratório no Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).
    5. Selecione **Pin tooDashboard** se pretender que um atalho de Olá laboratório tooappear no dashboard do portal Olá.
    6. Selecione **opções de automatização** modelos do Azure Resource Manager tooget para a automatização de configuração. 
    7. Selecione **Criar**. Depois de selecionar **criar**, Olá **DevTest Labs** apresenta do painel. Pode monitorizar Estado Olá Olá laboratório do processo de criação, observar Olá **notificações** área. Depois de concluída, atualização Olá página toosee Olá recém-criado laboratório na lista de Olá de laboratórios.  
    
    ![Painel Criar um laboratório](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Passos seguintes
Assim que tiver criado o seu laboratório, seguem-se algumas tooconsider passos seguinte:

* [Laboratório do acesso seguro tooa](devtest-lab-add-devtest-user.md).
* [Definir políticas de laboratório](devtest-lab-set-lab-policy.md).
* [Criar um modelo de laboratório](devtest-lab-create-template.md).
* [Criar artefactos personalizados para as suas VMs](devtest-lab-artifact-author.md).
* [Adicionar uma VM com o laboratório de tooa artefactos](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).

