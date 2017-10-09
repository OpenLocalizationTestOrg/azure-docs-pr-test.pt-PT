---
title: "aaaConfigure endereços IP privados para as VMs (clássica) - portal do Azure | Microsoft Docs"
description: "Saiba como endereços IP privados tooconfigure para máquinas virtuais (clássicas) utilizando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a>Configurar endereços IP privados para uma máquina virtual (clássica) utilizando Olá portal do Azure

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo abrange o modelo de implementação clássica Olá. Também pode [gerir um endereço IP privado estático no modelo de implementação do Resource Manager Olá](virtual-networks-static-private-ip-arm-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

passos de exemplo de Olá abaixo esperam num ambiente simple que já criado. Se pretender que os passos de Olá toorun como são apresentados neste documento, primeiro criar ambiente de teste de Olá descrito [criar uma vnet](virtual-networks-create-vnet-classic-pportal.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Como toospecify um privada endereços IP estáticos quando criar uma VM
toocreate uma VM chamada *DNS01* no Olá *front-end* sub-rede de uma VNet com o nome *TestVNet* com um IP privado estático de *192.168.1.101*, Siga os passos de Olá abaixo:

1. Num browser, navegue toohttp://portal.azure.com e, se necessário, inicie sessão com a sua conta do Azure.
2. Clique em **novo** > **computação** > **Windows Server 2012 R2 Datacenter**, tenha em atenção que Olá **selecionar um modelo de implementação** já lista mostra **clássico**e, em seguida, clique em **criar**.
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. No Olá **criar VM** painel, introduza o nome de Olá de Olá VM toobe criado (*DNS01* no nosso cenário), Olá conta de administrador local e a palavra-passe.
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. Clique em **configuração opcional** > **rede** > **rede Virtual**e, em seguida, clique em **TestVNet**. Se **TestVNet** não está disponível, certifique-se de que está a utilizar Olá *EUA Central* localização e tiver criado o ambiente de teste de Olá descrita no início de Olá deste artigo.
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. No Olá **rede** painel, marca de sub-rede Olá se, atualmente selecionada é *front-end*, em seguida, clique em **endereços IP**, em **aatribuiçãodeendereçosIP** clique **estático**e, em seguida, introduza *192.168.1.101* para **endereço IP** como mostrado abaixo.
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. Clique em **OK** no Olá **endereços IP** painel, em seguida, clique em **OK** no Olá **rede** painel e clique em **OK**no Olá **configuração opcional** painel.
7. No Olá **criar VM** painel, clique em **criar**. Tenha em atenção Olá mosaico abaixo apresentado no dashboard.
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Como as informações de uma VM do endereço IP privado estático de tooretrieve
tooview Olá privadas informações endereços IP estáticos para Olá VM criada com os passos de Olá acima, executar passos de Olá abaixo.

1. No portal do Azure do Azure Olá, clique em **Procurar tudo** > **máquinas virtuais (clássicas)** > **DNS01**  >   **Todas as definições** > **endereços IP** e repare Olá atribuição de endereços IP e o endereço IP, como mostrado abaixo.
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Como tooremove um privada endereços IP estáticos de uma VM
tooremove Olá endereço IP privado estático de Olá VM criada acima, siga os passos de Olá abaixo.

1. De Olá **endereços IP** painel mostrado acima, clique em **dinâmica** toohello à direita dos **atribuição de endereços IP**, em seguida, clique em **guardar**e, em seguida, Clique em **Sim**.
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Como tooadd um IP privado estático endereços tooan existente VM
tooadd um estático privada IP endereço toohello VM criada utilizando Olá passos acima, siga os passos de Olá abaixo:

1. De Olá **endereços IP** painel mostrado acima, clique em **estático** toohello à direita dos **atribuição de endereços IP**.
2. Tipo *192.168.1.101* para **endereço IP**, em seguida, clique em **guardar**e, em seguida, clique em **Sim**.

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [reservado de IP público](virtual-networks-reserved-public-ip.md) endereços.
* Saiba mais sobre [instância ao nível do IP público (ILPIP)](virtual-networks-instance-level-public-ip.md) endereços.
* Consulte Olá [as APIs REST do IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).

