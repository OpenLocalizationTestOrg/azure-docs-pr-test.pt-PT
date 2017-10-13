---
title: Gerir perfis no Traffic Manager do Azure | Microsoft Docs
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
ms.openlocfilehash: a5164282264124835692bc72a4ab61891aa7af9d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/11/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>Gerir um perfil no Traffic Manager do Azure

Os perfis do Gestor de Tráfego utilizam métodos de encaminhamento de tráfego para controlar a distribuição de tráfego para os seus serviços cloud ou pontos finais de Web site. Este artigo explica como criar e gerir estes perfis.

## <a name="create-a-traffic-manager-profile"></a>Criar um perfil do Gestor de Tráfego

Pode utilizar o portal do Azure para criar um perfil do Gestor de Tráfego. Depois de criar o perfil, pode configurar pontos finais, a monitorização e outras definições no portal do Azure. O Traffic Manager suporta até 200 pontos finais por perfil. No entanto, a maioria dos cenários de utilização exigem apenas alguns pontos finais.

### <a name="to-create-a-traffic-manager-profile"></a>Para criar um perfil do Gestor de Tráfego

1. Num browser, inicie sessão no [portal do Azure](http://portal.azure.com). Se ainda não tiver uma conta, pode inscrever-se para obter uma [avaliação gratuita durante um mês](https://azure.microsoft.com/free/). 
2. No menu **Hub**, clique em **Novo** > **Rede** > **Ver todos**, clique no perfil do **Gestor de Tráfego** para abrir o painel **Criar Perfil do Gestor de Tráfego** e clique em **Criar**.
3. No painel **Criar Perfil do Gestor de Tráfego**, preencha com o seguinte:
    1. Em **Nome**, indique um nome para o perfil. Este nome tem de ser exclusivo na zona trafficmanager.net e resultar no nome DNS <name>, trafficmanager.net, que é utilizado para aceder ao seu perfil do Gestor de Tráfego.
    2. Em **Método de encaminhamento**, selecione o método de encaminhamento **Prioridade**.
    3. Em **Subscrição**, selecione a subscrição na qual quer criar este perfil.
    4. Em **Grupo de Recursos**, crie um grupo de recursos novo onde colocar este perfil.
    5. Em **Localização do grupo de recursos**, selecione a localização do grupo de recursos. Esta definição refere-se à localização do grupo de recursos e não tem qualquer impacto no perfil do Gestor de Tráfego que vai ser implementado globalmente.
    6. Clique em **Criar**.
    7. Quando a implementação global do perfil do Gestor de Tráfego estiver concluída, é apresentada no respetivo grupo de recursos como um dos recursos.

## <a name="disable-enable-or-delete-a-profile"></a>Desativar, ativar ou eliminar um perfil

Pode desativar um perfil existente para que o Gestor de Tráfego não refira pedidos do utilizador aos pontos finais configurados. Quando desativa um perfil do Gestor de Tráfego, o perfil e as informações contidas no perfil permanecem intactos e podem ser editados na interface do Gestor de Tráfego.  As referências são retomadas quando voltar a ativar o perfil. Quando criar um perfil do Gestor de Tráfego no portal do Azure, este é ativado automaticamente. Se decidir que um perfil já não é necessário, poderá eliminá-lo.

### <a name="to-disable-a-profile"></a>Para desativar um perfil

1. Se estiver a utilizar um nome de domínio personalizado, altere o registo CNAME no seu servidor DNS da Internet, para que já não aponte para o seu perfil do Gestor de Tráfego.
2. O tráfego deixa de ser direcionado para os pontos finais através das definições de perfil do Gestor de Tráfego.
3. Num browser, inicie sessão no [portal do Azure](http://portal.azure.com).
2. Na barra de pesquisa do portal, procure o nome do **perfil do Gestor de Tráfego** que pretende modificar e, em seguida, clique no perfil do Gestor de Tráfego nos resultados apresentados.
3. No painel **Perfil do Gestor de Tráfego**, clique em **Descrição Geral** e, no painel Descrição Geral, clique em **Desativar** e confirme que pretende desativar o perfil do Gestor de Tráfego.

### <a name="to-enable-a-profile"></a>Para ativar um perfil

1. Num browser, inicie sessão no [portal do Azure](http://portal.azure.com).
2. Na barra de pesquisa do portal, procure o nome do **perfil do Gestor de Tráfego** que pretende modificar e, em seguida, clique no perfil do Gestor de Tráfego nos resultados apresentados.
3. No painel **Perfil do Gestor de Tráfego**, clique em **Descrição Geral** e, no painel Descrição Geral, clique em **Ativar**.
5. Se estiver a utilizar um nome de domínio personalizado, crie um registo de recursos CNAME no seu servidor DNS da Internet, para que aponte para o nome de domínio do perfil do Gestor de Tráfego.
6. O tráfego é direcionado para os pontos finais novamente.

### <a name="to-delete-a-profile"></a>Para eliminar um perfil

1. Certifique-se de que o registo de recursos DNS no servidor DNS de Internet já não utiliza um registo de recurso CNAME que aponta para o nome de domínio do perfil do Traffic Manager.
2. Na barra de pesquisa do portal, procure o nome do **perfil do Gestor de Tráfego** que pretende modificar e, em seguida, clique no perfil do Gestor de Tráfego nos resultados apresentados.
3. No painel **Perfil do Gestor de Tráfego**, clique em **Descrição Geral** e, no painel Descrição Geral, clique em **Eliminar** e confirme que pretende eliminar o perfil do Gestor de Tráfego.

## <a name="next-steps"></a>Passos seguintes

* [Adicionar um ponto final](traffic-manager-endpoints.md)
* [Configure Priority routing method](traffic-manager-configure-priority-routing-method.md) (Configurar o método de encaminhamento Prioritário)
* [Configure Geographic routing method](traffic-manager-configure-geographic-routing-method.md) (Configurar o método de encaminhamento Geográfico) 
* [Configure Weighted routing method](traffic-manager-configure-weighted-routing-method.md) (Configurar o método de encaminhamento Ponderado)
* [Configure Performance routing method](traffic-manager-configure-performance-routing-method.md) (Configurar o método de encaminhamento Desempenho)
