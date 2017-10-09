---
title: "método de encaminhamento utilizando o Gestor de tráfego do Azure de tráfego aaaConfigure geográfica | Microsoft Docs"
description: "Este artigo explica como tooconfigure Olá método de encaminhamento de tráfego geográfica utilizando o Gestor de tráfego do Azure"
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
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 4142389211ae54e7feea6564641e01e4477491e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-geographic-traffic-routing-method-using-traffic-manager"></a>Configurar o método de encaminhamento de tráfego geográfica de Olá utilizando o Gestor de tráfego

Olá método de encaminhamento de tráfego geográfica permite tráfego toodirect pontos finais toospecific com base na localização geográfica olá onde os pedidos de Olá têm origem. Este tutorial mostra como perfil de toocreate um Gestor de tráfego com este método de encaminhamento e configurar Olá pontos finais tooreceive o tráfego de localizações geográficas específicas.

## <a name="create-a-traffic-manager-profile"></a>Criar um perfil de Gestor de tráfego

1. Num browser, inicie sessão no toohello [portal do Azure](http://portal.azure.com). Se ainda não tiver uma conta, pode inscrever-se para obter uma [avaliação gratuita durante um mês](https://azure.microsoft.com/free/).
2. No menu do Hub de Olá, clique em **novo** > **redes** > **ver todos os**e, em seguida, clique em **perfil do Traffic Manager**tooopen Olá **perfil do Gestor de tráfego criar** painel.
3. No Olá **perfil do Gestor de tráfego criar** painel:
    1. Forneça um nome para o seu perfil. Este nome tem de toobe exclusivos numa zona de trafficmanager.net Olá e irá resultar no nome DNS Olá <profilename>, trafficmanager.net que irá ser utilizado tooaccess perfil do Traffic Manager.
    2. Selecione Olá **Geographic** método de encaminhamento.
    3. Selecione a subscrição de Olá que pretende toocreate este perfil em.
    4. Utilizar um grupo de recursos existente ou crie um novo tooplace de grupo de recursos este perfil em. Se optar por toocreate um novo grupo de recursos, utilize Olá **localização do grupo de recursos** localização de Olá toospecify pendente Olá do grupo de recursos. Esta definição refere-se a localização de toohello Olá do grupo de recursos e não tem impacto no Olá perfil do Traffic Manager que será implementada global.
    5. Depois de clicar em **criar**, perfil do Traffic Manager é criado e implementado global.

![Criar um perfil do Gestor de Tráfego](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a>Adicionar pontos finais

1. Pesquisar por nome de perfil do Traffic Manager Olá que acabou de criar na barra de pesquisa do portal de Olá e clique no resultado de Olá quando é mostrada.
2. Navegue demasiado**definições** -> **pontos finais** no painel de Gestor de tráfego de Olá.
3. Clique em **adicionar** tooshow Olá **adicionar ponto final** painel.
3. No Olá **pontos finais** painel, clique em **adicionar** e no Olá **adicionar ponto final** painel que é apresentado, concluir da seguinte forma:
4. Selecione **tipo** consoante o tipo de Olá do ponto final que está a adicionar. Para perfis de encaminhamento geográficas utilizadas na produção, recomendamos vivamente que tipos de ponto final aninhada que contenha um perfil de subordinados com mais do que um ponto final a utilizar. Para obter mais detalhes, consulte [perguntas mais frequentes sobre os métodos de encaminhamento de tráfego geográfica](traffic-manager-FAQs.md).
5. Forneça um **nome** através do qual pretende toorecognize este ponto final.
6. Determinados campos neste painel dependem do tipo de Olá do ponto final que está a adicionar:
    1. Se estiver a adicionar um ponto final do Azure, selecione Olá **tipo de recurso de destino** e Olá **destino** com base nos recursos de Olá pretende toodirect tráfego
    2. Se estiver a adicionar um **externo** ponto final, fornecer Olá **nome de domínio completamente qualificado (FQDN)** para o ponto final.
    3. Se estiver a adicionar um **aninhados endpoint**, selecione Olá **recurso de destino** que corresponde ao perfil de subordinados toohello pretende toouse e especifique Olá **decontagemdepontosfinaisdesubordinadosmínimo**.
7. Na secção de mapeamento de Georreplicação Olá, utilize Olá pendente regiões de Olá tooadd de onde pretende que o ponto final do tráfego toobe enviado toothis. Tem de adicionar pelo menos uma região e pode ter várias regiões mapeadas.
8. Repita esta para todos os pontos finais pretende tooadd sob este perfil

![Adicionar um ponto final do Gestor de tráfego](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Utilizar perfil do Traffic Manager Olá
1.  Na barra de pesquisa do portal de Olá, procure Olá **perfil do Traffic Manager** nome que criou no Olá anterior a secção e clique no perfil do Gestor de tráfego Olá no Olá resulta esse Olá apresentado.
2. No Olá **perfil do Traffic Manager** painel, clique em **descrição geral**.
3. Olá **perfil do Traffic Manager** painel apresenta o nome DNS de Olá do perfil do Traffic Manager recentemente criado. Isto pode ser utilizado por quaisquer clientes (por exemplo, ao navegar tooit utilizando um browser) tooget encaminhado toohello direita ponto final conforme determinado pela tipo Olá de encaminhamento.  No caso de Olá de encaminhamento geográfica, o Gestor de tráfego analisa Olá IP de origem do pedido de entrada Olá e determina a partir do qual é provenientes de região de Olá. Se nessa região endpoint tooan mapeada, o tráfego é encaminhado toothere. Se esta região não está mapeada tooan endpoint, em seguida, o Gestor de tráfego devolve uma resposta de consulta NODATA.

## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre [método de encaminhamento de tráfego Geographic](traffic-manager-routing-methods.md#geographic).
- Saiba como demasiado[testar as definições do Gestor de tráfego](traffic-manager-testing-settings.md).
