---
title: "os NSGs aaaManage utilizando Olá portal do Azure | Microsoft Docs"
description: "Saiba como toomanage existente NSGs utilizando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a>Gerir os NSGs através do portal Olá

> [!div class="op_single_selector"]
> * [Portal](virtual-network-manage-nsg-arm-portal.md)
> * [PowerShell](virtual-network-manage-nsg-arm-ps.md)
> * [CLI do Azure](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez do modelo de implementação clássica Olá.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a>Obter as informações
Pode ver os seus NSGs existentes, obter as regras para um NSG existente e descobrir os recursos que um NSG é associado a.

### <a name="view-existing-nsgs"></a>Ver os NSGs existentes

todos os tooview existente NSGs numa subscrição, Olá concluir os seguintes passos:

1. Num browser, navegue toohttp://portal.azure.com e, se necessário, inicie sessão com a sua conta do Azure.

2. Clique em **Procurar >** > **grupos de segurança de rede**.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. Verifique a lista de Olá de NSGs em Olá **grupos de segurança de rede** painel.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a>Vista NSGs num grupo de recursos

lista de Olá tooview de NSGs em Olá **RG NSG** grupo de recursos, Olá concluir os seguintes passos:

1. Clique em **grupos de recursos >** > **RG NSG** > **...** .

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. Na lista de Olá de recursos, procure itens a apresentar o ícone NSG Olá, conforme mostrado no Olá **recursos** painel abaixo.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a>Listar todas as regras para um NSG

regras de Olá tooview de um NSG denominado **NSG-front-end**, completa Olá os seguintes passos:

1. De Olá **grupos de segurança de rede** painel ou Olá **recursos** painel mostrado acima, clique em **NSG-front-end**.

2. No Olá **definições** separador, clique em **regras de segurança de entrada**.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. Olá **regras de segurança de entrada** painel é apresentado como mostrado abaixo.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. No Olá **definições** separador, clique em **regras de segurança de saída** toosee Olá regras de saída.

    > [!NOTE]
    > regras de predefinidas tooview, clique em Olá **predefinido regras** ícone, Olá parte superior do painel de Olá que apresenta as regras de Olá.
    >

### <a name="view-nsgs-associations"></a>Ver as associações de NSGs

tooview que Olá recursos **NSG-front-end** NSG é Olá associar com, concluir os seguintes passos:

1. De Olá **grupos de segurança de rede** painel ou Olá **recursos** painel mostrado acima, clique em **NSG-front-end**.

2. No Olá **definições** separador, clique em **sub-redes** tooview são as sub-redes associados toohello NSG.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. No Olá **definições** separador, clique em **interfaces de rede** tooview que estão associados NICs toohello NSG.

## <a name="manage-rules"></a>Gerir as regras
Pode adicionar tooan regras existentes NSG, editar regras existentes e remova regras.

### <a name="add-a-rule"></a>Adicionar uma regra
tooadd uma regra que permite **entrada** tráfego tooport **443** de qualquer máquina toohello **NSG-front-end** NSG, Olá concluir os seguintes passos:

1. De Olá **grupos de segurança de rede** painel ou Olá **recursos** painel mostrado acima, clique em **NSG-front-end**.
2. No Olá **definições** separador, clique em **regras de segurança de entrada**.
3. No Olá **regras de segurança de entrada** painel, clique em **adicionar**. Em seguida, no Olá **Adicionar regra de segurança de entrada** painel, preencher valores de Olá, conforme mostrado abaixo e, em seguida, clique em **OK**.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    Após alguns segundos, repare a nova regra de Olá no Olá **regras de segurança de entrada** painel.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a>Alterar uma regra
regra de Olá toochange criada acima tooallow de entrada do tráfego de Olá **Internet** Olá concluída, apenas os seguintes passos:

1. De Olá **grupos de segurança de rede** painel ou Olá **recursos** painel mostrado acima, clique em **NSG-front-end**.
2. No Olá **definições** separador, clique em regras de Olá criada acima.
3. No Olá **https permitir** painel, alteração Olá **origem** propriedade conforme mostrado abaixo e, em seguida, clique em **guardar**.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a>Eliminar uma regra

toodelete Olá regra criado acima, completa Olá os seguintes passos:

1. De Olá **grupos de segurança de rede** painel ou Olá **recursos** painel mostrado acima, clique em **NSG-front-end**.
2. No Olá **definições** separador, clique em regras de Olá criada acima.
3. No Olá **https permitir** painel, clique em **eliminar**e, em seguida, clique em **Sim**.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a>Gerir as associações
Pode associar um NSG toosubnets e NICs. Também pode desassociar um NSG a partir de qualquer recurso que está associado.

### <a name="associate-an-nsg-tooa-nic"></a>Associar um NSG tooa NIC
Olá tooassociate **NSG-front-end** NSG toohello **TestNICWeb1** NIC, Olá concluir os seguintes passos:

1. De Olá **grupos de segurança de rede** painel ou Olá **recursos** painel mostrado acima, clique em **NSG-front-end**.
2. No Olá **definições** separador, clique em **interfaces de rede** > **associar** > **TestNICWeb1**.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a>Desassociar um NSG a partir de uma NIC

Olá toodissociate **NSG-front-end** NSG de Olá **TestNICWeb1** NIC, Olá concluir os seguintes passos:

1. No portal do Azure Olá, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **TestNICWeb1**.

2. No Olá **TestNICWeb1** painel, clique em **alterar segurança...**   >  **Nenhum**.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> Também pode utilizar este painel tooassociate Olá NIC tooany existente NSG.
>

### <a name="dissociate-an-nsg-from-a-subnet"></a>Desassociar um NSG de sub-rede

Olá toodissociate **NSG-front-end** NSG de Olá **front-end** sub-rede, Olá concluir os seguintes passos:

1. No portal do Azure Olá, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **TestVNet**.

2. No Olá **definições** painel, clique em **sub-redes** > **front-end** > **grupo de segurança de rede**  >  **Nenhum**.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. No Olá **front-end** painel, clique em **guardar**.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a>Associar uma sub-rede de tooa NSG

Olá tooassociate **NSG-front-end** NSG toohello **FronEnd** sub-rede novamente, Olá concluir os seguintes passos:

1. No portal do Azure Olá, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **TestVNet**.
2. No Olá **definições** painel, clique em **sub-redes** > **front-end** > **grupo de segurança de rede**  >  **NSG-front-end**.
3. No Olá **front-end** painel, clique em **guardar**.

> [!NOTE]
> Também pode associar uma sub-rede de tooa NSG das thh NSG **definições** painel.
>

## <a name="delete-an-nsg"></a>Eliminar um NSG
Só é possível eliminar um NSG se tooany recurso não está associado. toodelete um NSG, Olá concluir os passos seguintes:.

1. No portal do Azure Olá, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **NSG-front-end**.
2. No Olá **definições** painel, clique em **interfaces de rede**.
3. Se existirem quaisquer NICs listados, clique em Olá NIC e siga o passo 2 [desassociar um NSG a partir de uma NIC](#Dissociate-an-NSG-from-a-NIC).
4. Repita o passo 3 para cada NIC.
5. No Olá **definições** painel, clique em **sub-redes**.
6. Se existirem quaisquer sub-redes listados, clique em sub-rede Olá e siga os passos 2 e 3 na [desassociar um NSG de sub-rede](#Dissociate-an-NSG-from-a-subnet).
7. Desloca toohello esquerdo **NSG-front-end** painel, em seguida, clique em **eliminar** > **Sim**.

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a>Passos seguintes
* [Ativar o registo](virtual-network-nsg-manage-log.md) para NSGs.
