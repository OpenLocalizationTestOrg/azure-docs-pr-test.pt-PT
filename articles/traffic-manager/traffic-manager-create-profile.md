---
title: aaaCreate um perfil do Traffic Manager no Azure | Microsoft Docs
description: Este artigo descreve como toocreate um perfil do Traffic Manager
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: kumud
ms.openlocfilehash: 5cd3d2903552c9a0427da41a73f6f38f6b0afc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-traffic-manager-profile"></a>Criar um perfil do Gestor de Tráfego

Este artigo descreve como um perfil com **prioridade** tipo de encaminhamento pode ser criado pontos finais do tooroute utilizadores tootwo Web Apps do Azure. Ao utilizar Olá **prioridade** encaminhamento tipo, todo o tráfego é encaminhado toohello primeiro ponto final enquanto Olá segundo é guardada como uma cópia de segurança. Como resultado, os utilizadores podem ser encaminhados toohello segundo ponto final, se o primeiro ponto de final Olá fica em mau estado de funcionamento.

Neste artigo, criados anteriormente dois pontos finais de aplicação Web do Azure são perfil do Traffic Manager associadas toothis recentemente criado. toolearn mais informações sobre como pontos finais de aplicação Web do Azure toocreate, visite Olá [página de documentação de Web Apps do Azure](https://docs.microsoft.com/azure/app-service-web/). Pode adicionar qualquer ponto final que tem um nome DNS e é acessível através da internet pública e que estamos a utilizar pontos finais de Web Apps do Azure como um exemplo de Olá.

### <a name="create-a-traffic-manager-profile"></a>Criar um perfil do Gestor de Tráfego
1. Num browser, inicie sessão no toohello [portal do Azure](http://portal.azure.com). Se ainda não tiver uma conta, pode inscrição para uma [um mês avaliação gratuita](https://azure.microsoft.com/free/). 
2. No Olá **Hub** menu, clique em **novo** > **redes** > **ver todos os**, clique em **tráfego Gestor de** Olá do perfil tooopen **perfil do Gestor de tráfego criar** painel, em seguida, clique em **criar**.
3. No Olá **perfil do Gestor de tráfego criar** painel, concluída, da seguinte forma:
    1. Em **Nome**, indique um nome para o perfil. Este nome tem de toobe exclusivos numa zona de trafficmanager.net Olá e resulta num nome DNS Olá <name>, trafficmanager.net que é utilizado tooaccess perfil do Traffic Manager.
    2. No **método de encaminhamento**, selecione Olá **prioridade** método de encaminhamento.
    3. No **subscrição**, selecione a subscrição Olá pretende toocreate este perfil em
    4. No **grupo de recursos**, criar um novo tooplace de grupo de recursos este perfil em.
    5. No **localização do grupo de recursos**, selecione a localização de Olá Olá do grupo de recursos. Esta definição refere-se a localização de toohello Olá do grupo de recursos e não tem impacto no Olá perfil do Traffic Manager que será implementada global.
    6. Clique em **Criar**.
    7. Quando a implementação de global Olá do perfil do Traffic Manager estiver concluída, este está listado no grupo de recursos do respetivo como um dos recursos de Olá.

    ![Criar um perfil do Gestor de Tráfego](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a>Adicionar pontos finais do Gestor de tráfego

1. Na barra de pesquisa do portal de Olá, procure Olá **perfil do Traffic Manager** nome que criou no Olá anterior a secção e clique em perfil do Gestor de tráfego Olá no Olá resulta esse Olá apresentado.
2. No Olá **perfil do Traffic Manager** painel, no Olá **definições** secção, clique em **pontos finais**.
3. No Olá **pontos finais** painel que é apresentado, clique em **adicionar**.
4. No Olá **adicionar ponto final** painel, concluída, da seguinte forma:
    1. Em **Tipo**, clique em **Ponto final do Azure**.
    2. Forneça um **nome** através do qual pretende toorecognize este ponto final.
    3. Para **tipo de recurso de destino**, clique em **do serviço de aplicações**.
    4. Para **recurso de destino**, clique em **escolher um serviço de aplicações** listagem de Olá tooshow de Olá aplicações Web em Olá mesma subscrição. No Olá **recursos** painel que é apresentado, escolha Olá que pretende que tooadd como Olá primeiro ponto final do serviço de aplicações.
    5. Em **Prioridade**, selecione **1**. Isto resulta em todo o tráfego destinado toothis endpoint se está em bom estado.
    6. Mantenha a caixa **Adicionar como desativado** desmarcada.
    7. Clique em **OK**
5.  Repita os passos 3 e 4 para o ponto de final Olá seguinte Web Apps do Azure. Certifique-se de que tooadd-lo com o respetivo **prioridade** valor definido em **2**.
6.  Quando a adição de Olá de ambos os pontos finais estiver concluída, estes são apresentados na Olá **perfil do Traffic Manager** painel, juntamente com o respetivo estado de monitorização como **Online**.

    ![Adicionar um ponto final do Gestor de tráfego](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Utilizar perfil do Traffic Manager Olá
1.  Na barra de pesquisa do portal de Olá, procure Olá **perfil do Traffic Manager** nome que criou no Olá anterior a secção. Nos resultados de Olá que são apresentados, clique em perfil do Gestor de tráfego de Olá.
2. No Olá **perfil do Traffic Manager** painel, clique em **descrição geral**.
3. Olá **perfil do Traffic Manager** painel apresenta o nome DNS de Olá do perfil do Traffic Manager recentemente criado. Isto pode ser utilizado por quaisquer clientes (por exemplo, ao navegar tooit utilizando um browser) tooget encaminhado toohello direita ponto final conforme determinado pela tipo Olá de encaminhamento. Neste caso, todos os pedidos são encaminhadas toohello primeiro ponto final e se o Gestor de tráfego detetar-ser mau estado de funcionamento, o tráfego de Olá automaticamente a ativação pós-falha toohello próximo ponto final.

## <a name="delete-hello-traffic-manager-profile"></a>Eliminar perfil do Gestor de tráfego de Olá
Quando já não é necessário, elimine o grupo de recursos de Olá e o perfil do Traffic Manager Olá que criou. toodo por isso, selecione o grupo de recursos de Olá Olá **perfil do Traffic Manager** painel e clique em **eliminar**.

## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre [tipos de encaminhamento](traffic-manager-routing-methods.md).
- Saiba mais sobre os tipos de ponto final [tipos de ponto final](traffic-manager-endpoint-types.md).
- Saiba mais sobre [monitorização de pontos finais](traffic-manager-monitoring.md).



