---
title: "endereços IP aaaMultiple máquinas virtuais do Azure - Portal | Microsoft Docs"
description: "Saiba como tooassign vários de endereços IP através de máquina virtual tooa Olá portal do Azure | Gestor de recursos."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: 34075766ac68c8de38c258a4d70e35881f28bb0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-portal"></a>Atribuir várias máquinas de toovirtual do endereços IP utilizando Olá portal do Azure

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
Este artigo explica como toocreate uma máquina virtual (VM) através de Olá do Azure Resource Manager implementação modelo utilizando Olá portal do Azure. Vários endereços IP não não possível atribuir tooresources criados através do modelo de implementação clássica Olá. mais informações sobre modelos de implementação do Azure, leia Olá toolearn [compreender os modelos de implementação](../resource-manager-deployment-model.md) artigo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Criar uma VM com vários endereços IP

Se quiser toocreate uma VM com vários endereços IP ou um endereço IP privado estático, tem de criar, utilizar o PowerShell ou Olá CLI do Azure. Clique em Olá PowerShell ou as opções de CLI, Olá parte superior do toolearn artigo como. Pode criar uma VM com um único endereço IP privado dinâmico e (opcionalmente) um único endereço IP público com o portal de Olá seguindo os passos de Olá em Olá [criar uma VM do Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) ou [criar uma VM com Linux](../virtual-machines/linux/quick-create-portal.md) artigos. Depois de criar Olá VM, pode alterar o tipo de endereço IP de Olá de toostatic dinâmica e adicionar endereços IP adicionais através do portal Olá pelos seguintes passos Olá [Adicionar IP endereços tooa VM](#add) secção deste artigo.

## <a name="add"></a>Adicionar endereços IP tooa VM

Pode adicionar pública e privada tooa de endereços IP NIC, concluindo Olá passos que se seguem. Olá exemplos Olá secções a seguir partem do princípio de que já tem uma VM com as configurações de IP de Olá três descritas Olá [cenário](#Scenario) deste artigo, mas não é necessário que efetuar.

### <a name="coreadd"></a>Passos de núcleo

1. Procure toohello do portal do Azure em https://portal.azure.com e inicie sessão para a mesma, se necessário.
2. No portal de Olá, clique em **mais serviços** > tipo *máquinas virtuais* no Olá caixa do filtro e, em seguida, clique em **máquinas virtuais**.
3. No Olá **máquinas virtuais** painel, clique em Olá VM pretende tooadd IP endereços. Clique em **interfaces de rede** no painel de máquina virtual de Olá que aparece e, em seguida, selecione de Olá rede interface pretende tooadd Olá IP endereços. No exemplo de Olá apresentado na Olá na seguinte imagem, Olá NIC com o nome *myNIC* da VM com o nome de Olá *myVM* está selecionado:

    ![Interface de rede](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. No Olá painel que aparece Olá NIC que selecionou, clique em **configurações de IP**.

Olá concluir os passos de uma das seguintes secções Olá que se seguem, com base no tipo de Olá do endereço IP que pretende tooadd.

### <a name="add-a-private-ip-address"></a>**Adicionar um endereço IP privado**

Conclua os seguintes passos tooadd um novo endereço IP privado de Olá:

1. Olá concluir os passos em Olá [principais passos](#coreadd) secção deste artigo.
2. Clique em **Adicionar**. No Olá **configuração de IP adicionar** painel que aparece, criar uma configuração de IP com o nome *IPConfig 4* com *10.0.0.7* como um *estático* IP privado de endereços, em seguida, clique em **OK**.

    > [!NOTE]
    > Ao adicionar um endereço IP estático, tem de especificar um endereço não utilizado, válido Olá de sub-rede Olá que NIC está ligado. Se o endereço de Olá que selecionar não estiver disponível, portal Olá irá mostrar um X para o endereço IP Olá e terá tooselect outro.

3. Assim que clicar em OK, o painel Olá será fechado e verá Olá nova configuração de IP listada. Clique em **OK** tooclose Olá **configuração de IP adicionar** painel.
4. Pode clicar em **adicionar** tooadd configurações de IP adicionais, ou feche abrir todos os endereços IP adicionar toofinish painéis.
5. Adicionar Olá privada IP endereços toohello VM sistema concluindo Olá os passos para o sistema operativo no Olá [IP adicionar endereços de sistema de operativo tooa VM](#os-config) secção deste artigo.

### <a name="add-a-public-ip-address"></a>Adicionar um endereço IP público

Um endereço IP público é adicionado ao associar um tooeither de recursos de endereço IP público, uma nova configuração de IP ou uma configuração de IP existente.

> [!NOTE]
> Endereços IP públicos têm uma taxa nominal. toolearn mais informações sobre IP endereços preços, leia Olá [preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Não há limite toohello diversas endereços IP públicos que podem ser utilizadas numa subscrição. mais informações sobre limites de Olá, leia Olá toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.
> 

### <a name="create-public-ip"></a>Criar um recurso de endereço IP público

Um endereço IP público é uma definição para um recurso de endereço IP público. Se tiver um recurso de endereço IP público que não é uma configuração de IP tooan atualmente associados que pretende tooassociate tooan, ignorar Olá os seguintes passos e à configuração IP de concluir os passos de Olá de uma das seguintes secções Olá que se seguem, conforme necessita. Se não tiver um recurso de endereço IP público disponível, conclua Olá toocreate passos um a seguir:

1. Procure toohello do portal do Azure em https://portal.azure.com e inicie sessão para a mesma, se necessário.
3. No portal de Olá, clique em **novo** > **redes** > **endereço IP público**.
4. No Olá **Criar endereço IP público** painel apresentado, introduza um **nome**, selecione um **atribuição de endereços IP** tipo, um **subscrição**, um **Grupo de recursos**e um **localização**, em seguida, clique em **criar**, conforme apresentado na Olá seguinte imagem:

    ![Criar um recurso de endereço IP público](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. Olá concluir os passos de uma das seguintes secções de Olá que se seguem tooassociate Olá pública recursos tooan IP configuração do endereço IP.

#### <a name="associate-hello-public-ip-address-resource-tooa-new-ip-configuration"></a>Associar Olá pública recursos tooa novo IP configuração do endereço IP

1. Olá concluir os passos em Olá [principais passos](#coreadd) secção deste artigo.
2. Clique em **Adicionar**. No Olá **configuração de IP adicionar** painel que aparece, criar uma configuração de IP com o nome *IPConfig 4*. Ativar Olá **endereço IP público** e selecione um existente, disponível endereço recurso de IP público de Olá **escolher endereço IP público** painel que aparece.

    Depois de selecionar recurso de endereço IP público Olá, clique em **OK** e painel Olá será fechada. Se não tiver um endereço IP público existente, pode criar um, efetuando os passos de Olá Olá [criar um recurso de endereço IP público](#create-public-ip) secção deste artigo. 

3. Reveja Olá nova configuração de IP. Apesar de explicitamente não foi atribuído um endereço IP privado, um foi atribuído automaticamente toohello configuração de IP, porque todas as configurações de IP tem de ter um endereço IP privado.
4. Pode clicar em **adicionar** tooadd configurações de IP adicionais, ou feche abrir todos os endereços IP adicionar toofinish painéis.
5. Adicionar Olá privado IP endereço toohello VM sistema operativo, concluindo Olá passos para o seu sistema operativo no Olá [IP adicionar endereços de sistema de operativo tooa VM](#os-config) secção deste artigo. Não adicione Olá público IP endereço toohello sistema operativo.

#### <a name="associate-hello-public-ip-address-resource-tooan-existing-ip-configuration"></a>Associar Olá pública recursos tooan existente IP configuração do endereço IP

1. Olá concluir os passos em Olá [principais passos](#coreadd) secção deste artigo.
2. Clique em configuração de IP Olá que pretende tooadd Olá endereço recurso de IP público para.
3. No painel de IPConfig Olá que aparece, clique em **endereço IP**.
4. No Olá **escolher endereço IP público** painel que aparece, selecione um endereço IP público.
5. Clique em **guardar** e painéis de Olá serão fechada. Se não tiver um endereço IP público existente, pode criar um, efetuando os passos de Olá Olá [criar um recurso de endereço IP público](#create-public-ip) secção deste artigo.
3. Reveja Olá nova configuração de IP.
4. Pode clicar em **adicionar** tooadd configurações de IP adicionais, ou feche abrir todos os endereços IP adicionar toofinish painéis. Não adicione Olá público IP endereço toohello sistema operativo.


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
