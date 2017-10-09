---
title: perfis do Traffic Manager do Azure de aaaManage | Microsoft Docs
description: "Este artigo ajuda-o a criar, desativar, ativar e eliminar perfis do Gestor de Tráfego do Azure."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: 0c6ab0c451581d039514a9de0b525b3937e45a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>Gerir um perfil no Traffic Manager do Azure

Perfis do Traffic Manager utilizam o encaminhamento de tráfego métodos toocontrol Olá distribuição dos serviços de nuvem de tooyour de tráfego ou pontos finais do Web site. Este artigo explica como toocreate e gere estes perfis.

## <a name="create-a-traffic-manager-profile"></a>Criar um perfil do Gestor de Tráfego

Pode criar um perfil de Gestor de tráfego utilizando Olá portal do Azure. Depois de criar o perfil, pode configurar pontos finais, a monitorização e outras definições no Olá portal do Azure. Gestor de tráfego suporta até pontos finais de too200 por perfil. No entanto, a maioria dos cenários de utilização exigem apenas alguns pontos finais.

### <a name="toocreate-a-traffic-manager-profile"></a>toocreate um perfil do Traffic Manager

1. Num browser, inicie sessão no toohello [portal do Azure](http://portal.azure.com). Se ainda não tiver uma conta, pode inscrever-se para obter uma [avaliação gratuita durante um mês](https://azure.microsoft.com/free/). 
2. No Olá **Hub** menu, clique em **novo** > **redes** > **ver todos os**, clique em **tráfego Gestor de** Olá do perfil tooopen **perfil do Gestor de tráfego criar** painel, em seguida, clique em **criar**.
3. No Olá **perfil do Gestor de tráfego criar** painel, concluída, da seguinte forma:
    1. Em **Nome**, indique um nome para o perfil. Este nome tem de toobe exclusivos numa zona de trafficmanager.net Olá e resulta num nome DNS Olá <name>, trafficmanager.net, que é utilizado tooaccess perfil do Traffic Manager.
    2. No **método de encaminhamento**, selecione Olá **prioridade** método de encaminhamento.
    3. No **subscrição**, selecione a subscrição Olá pretende toocreate este perfil em
    4. No **grupo de recursos**, criar um novo tooplace de grupo de recursos este perfil em.
    5. No **localização do grupo de recursos**, selecione a localização de Olá Olá do grupo de recursos. Esta definição refere-se a localização de toohello Olá do grupo de recursos e não tem impacto no Olá perfil do Traffic Manager que será implementada global.
    6. Clique em **Criar**.
    7. Quando a implementação de global Olá do perfil do Traffic Manager estiver concluída, este está listado no grupo de recursos do respetivo como um dos recursos de Olá.

## <a name="disable-enable-or-delete-a-profile"></a>Desativar, ativar ou eliminar um perfil

Pode desativar um perfil existente para que esse gestor de tráfego não se refere a pontos finais de toohello configurado de pedidos de utilizador. Ao desativar um perfil do Traffic Manager, o perfil de Olá e informações de Olá contido no perfil de Olá permanecem intactas e podem ser editados na interface do Gestor de tráfego de Olá.  As referências retomar quando voltar a ativar o perfil de Olá. Quando cria um perfil do Traffic Manager no Olá portal do Azure, é ativada automaticamente. Se decidir que um perfil já não é necessário, poderá eliminá-lo.

### <a name="toodisable-a-profile"></a>toodisable um perfil

1. Se estiver a utilizar um nome de domínio personalizado, altere o registo CNAME Olá no seu servidor DNS da Internet para que aponte tooyour perfil de Gestor de tráfego já não.
2. Deixa de tráfego a ser direcionado pontos finais de toohello através das definições de perfil do Gestor de tráfego Olá.
3. Num browser, inicie sessão no toohello [portal do Azure](http://portal.azure.com).
2. Na barra de pesquisa do portal de Olá, procure Olá **perfil do Traffic Manager** nome que pretende toomodify e, em seguida, clique em perfil do Traffic Manager Olá no Olá resulta esse Olá apresentado.
3. No Olá **perfil do Traffic Manager** painel, clique em **descrição geral**, no painel de descrição geral de Olá clique **desativar**e, em seguida, confirme o perfil de Gestor de tráfego de Olá toodisable.

### <a name="tooenable-a-profile"></a>tooenable um perfil

1. Num browser, inicie sessão no toohello [portal do Azure](http://portal.azure.com).
2. Na barra de pesquisa do portal de Olá, procure Olá **perfil do Traffic Manager** nome que pretende toomodify e, em seguida, clique em perfil do Traffic Manager Olá no Olá resulta esse Olá apresentado.
3. No Olá **perfil do Traffic Manager** painel, clique em **descrição geral**e, em seguida, no painel de descrição geral de Olá clique **ativar**.
5. Se estiver a utilizar um nome de domínio personalizado, crie um registo de recurso CNAME no seu nome de domínio do DNS da Internet server toopoint toohello do perfil do Traffic Manager.
6. O tráfego é pontos finais de toohello direcionados novamente.

### <a name="toodelete-a-profile"></a>toodelete um perfil

1. Certifique-se de que o registo de recursos DNS Olá no seu servidor DNS de Internet já não utiliza um registo de recurso CNAME que aponta toohello o nome de domínio do perfil do Traffic Manager.
2. Na barra de pesquisa do portal de Olá, procure Olá **perfil do Traffic Manager** nome que pretende toomodify e, em seguida, clique em perfil do Traffic Manager Olá no Olá resulta esse Olá apresentado.
3. No Olá **perfil do Traffic Manager** painel, clique em **descrição geral**, no painel de descrição geral de Olá clique **eliminar**e, em seguida, confirme o perfil de Gestor de tráfego de Olá toodelete.

## <a name="next-steps"></a>Passos seguintes

* [Adicionar um ponto final](traffic-manager-endpoints.md)
* [Configure Priority routing method](traffic-manager-configure-priority-routing-method.md) (Configurar o método de encaminhamento Prioritário)
* [Configure Geographic routing method](traffic-manager-configure-geographic-routing-method.md) (Configurar o método de encaminhamento Geográfico) 
* [Configure Weighted routing method](traffic-manager-configure-weighted-routing-method.md) (Configurar o método de encaminhamento Ponderado)
* [Configure Performance routing method](traffic-manager-configure-performance-routing-method.md) (Configurar o método de encaminhamento Desempenho)
