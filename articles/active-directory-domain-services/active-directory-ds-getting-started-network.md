---
title: "Serviços de domínio do Azure Active Directory: Introdução | Microsoft Docs"
description: "Ativar o Azure Active Directory Domain Services utilizando Olá portal do Azure (pré-visualização)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Ativar o Azure Active Directory Domain Services utilizando Olá portal do Azure (pré-visualização)


## <a name="before-you-begin"></a>Antes de começar
Consulte demasiado[considerações de redes para o Azure Active Directory Domain Services](active-directory-ds-networking.md).


## <a name="task-2-configure-network-settings"></a>Tarefa 2: Configurar definições de rede
tarefa de configuração seguinte Olá é toocreate uma Azure virtual network e uma sub-rede dedicada dentro da mesma. O Azure Active Directory Domain Services é ativado nesta sub-rede dentro da sua rede virtual. Também pode escolher uma rede virtual existente e criar a sub-rede Olá dedicado dentro da mesma.

1. Clique em **rede Virtual** tooselect uma rede virtual.
2. No Olá **escolha de rede virtual** painel, pode ver todas as redes virtuais existentes. Consulte apenas Olá redes virtuais que pertencem toohello grupo de recursos e localização do Azure que selecionou no Olá **Noções básicas** página do assistente.

3. Escolha a rede virtual Olá em que os serviços de domínio do Azure AD devem ser ativados. Clique em **criar nova**, se preferir toocreate uma nova rede virtual. Recomendamos vivamente a utilização de uma sub-rede dedicada para os serviços de domínio do Azure AD. Se escolher uma rede virtual existente, [criar uma sub-rede dedicada utilizando a extensão de redes virtuais Olá](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) e, em seguida, escolha dessa sub-rede. 

    ![Escolha a rede virtual](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. Clique em **sub-rede** toopick Olá dedicado sub-rede nesta rede virtual, no qual tooenable a nova geridos por domínio. No Olá **criar sub-rede** painel, especifique um nome para a sub-rede de Olá e clique em **OK** quando tiver terminado. Por exemplo, crie uma sub-rede com o nome de Olá 'DomainServices', tornando mais fácil para os outro administradores toounderstand o que é implementado dentro de sub-rede Olá.

    ![Escolha a sub-rede numa rede virtual Olá](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **Diretrizes para selecionar uma sub-rede**
  > 1. Utilize uma sub-rede dedicada para os serviços de domínio do Azure AD. Não implemente quaisquer outra máquinas virtuais toothis sub-rede. Esta configuração permite-lhe tooconfigure grupos de segurança de rede (NSGs) para as suas máquinas virtuais/cargas de trabalho sem perturbar o seu domínio gerido. Para obter mais informações, consulte [redes considerações para o Azure Active Directory Domain Services](active-directory-ds-networking.md).
  2. Não selecione a sub-rede do Gateway Olá para implementar os serviços de domínio do Azure AD, porque não é uma configuração suportada.
  3. Certifique-se de que essa sub-rede de Olá que selecionou tem suficiente espaço de endereço disponível - endereços IP disponíveis, pelo menos, 3 a 5.
  >

5. Quando tiver terminado, clique em **OK** toomove no toohello **grupo Administrador** página do Assistente de Olá.


## <a name="next-step"></a>Passo seguinte
[Tarefa 3: configurar o grupo administrativo e ativar os serviços de domínio do Azure AD](active-directory-ds-getting-started-admingroup.md)
