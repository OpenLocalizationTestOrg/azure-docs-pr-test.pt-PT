---
title: aaaManage DNS zonas no DNS do Azure - portal do Azure | Microsoft Docs
description: "Pode gerir zonas DNS utilizando Olá portal do Azure. Este artigo descreve como tooupdate, eliminar e criar zonas DNS no DNS do Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a>Como toomanage zonas de DNS no Olá portal do Azure

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [CLI do Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-operations-dnszones-cli.md)

Este artigo mostra como toomanage seu DNS zonas utilizando Olá portal do Azure. Também pode gerir as zonas DNS utilizando Olá plataforma [CLI do Azure](dns-operations-dnszones-cli.md) ou Olá Azure [PowerShell](dns-operations-dnszones.md).

## <a name="create-a-dns-zone"></a>Criar uma zona DNS

1. A iniciar sessão toohello portal do Azure
2. No menu do Hub de Olá, clique em e clique em **novo > rede >** e, em seguida, clique em **zona DNS** painel do tooopen Olá criar DNS zona.

    ![Zona DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. No Olá **zona DNS criar** painel introduza Olá valores a seguir, em seguida, clique em **criar**:


   | **Definição** | **Valor** | **Detalhes** |
   |---|---|---|
   |**Nome**|contoso.com|nome de Olá da zona DNS de Olá|
   |**Subscrição**|[A sua subscrição]|Selecione uma zona DNS de Olá toocreate subscrição no.|
   |**Grupo de recursos**|**Criar novo:** contosoDNSRG|Crie um grupo de recursos. nome do grupo de recursos de Olá têm de ser exclusivo dentro da subscrição Olá que selecionou. mais informações sobre grupos de recursos, leia Olá toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artigo de descrição geral.|
   |**Localização**|EUA Oeste||

> [!NOTE]
> grupo de recursos de Olá refere-se a localização de toohello Olá do grupo de recursos e não tem impacto na zona DNS Olá. localização de zona DNS Olá está sempre "global" e não é apresentada.

## <a name="list-dns-zones"></a>Zonas DNS de lista

No portal do Azure de Olá, navegue demasiado**mais serviços** > **redes** > **zonas DNS**. Cada zona DNS é é seus próprios recursos, informações como o número de conjuntos de registos e servidores de nomes são visíveis desta vista. coluna Olá **servidores de nomes** não se encontra na vista de predefinição Olá, tooadd clique **colunas**, selecione **nome servidores** e clique em **feito**.

![listar zonas DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a>Eliminar uma zona DNS

Navegue tooa zona DNS no portal de Olá. No Olá **zona DNS** painel, clique em **eliminar zona**. São tooconfirm pedido são intenção zona DNS de Olá toodelete. Também eliminar uma zona DNS elimina todos os registos de Olá que estão contidos na zona de Olá.

## <a name="next-steps"></a>Passos seguintes

Saiba como toowork com a sua zona DNS e os registos, visitando [introdução ao DNS do Azure utilizando o portal do Azure de Olá](dns-getstarted-portal.md).
