---
title: "Criar uma instância da Gestão de API do Azure | Microsoft Docs"
description: "Siga os passos deste tutorial para criar uma nova instância da Gestão de API do Azure."
services: api-management
documentationcenter: 
author: juliako
manager: cflower
editor: 
ms.service: api-management
ms.workload: integration
ms.topic: quickstart
ms.custom: mvc
ms.date: 11/28/2017
ms.author: apimpm
ms.openlocfilehash: b7ea43419cbbb5f5d38f8ad721d564650c3681a6
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="create-a-new-azure-api-management-service-instance"></a>Criar uma nova instância de serviço da Gestão de API do Azure

A Gestão de API (APIM) do Azure ajuda as organizações a publicar APIs para programadores externos, parceiros e internos, de modo a que estes possam explorar ao máximo o potencial dos seus dados e serviços. A Gestão de API fornece as competências essenciais para garantir um programa de API bem-sucedido através do envolvimento dos programadores, das informações de negócio, da análise, da segurança e da proteção. A APIM permite-lhe criar e gerir gateways de API modernos para serviços de back-end existentes alojados em qualquer lado. Para obter mais informações, consulte o tópico [Descrição Geral](api-management-key-concepts.md).

Este início rápido descreve os passos para a criação de uma nova instância de serviço da Gestão de API através do portal do Azure.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

![nova instância](./media/get-started-create-service-instance/get-started-create-service-instance-created.png)

## <a name="log-in-to-azure"></a>Iniciar sessão no Azure

Inicie sessão no portal do Azure em http://portal.azure.com.

## <a name="create-a-new-service"></a>Criar um novo serviço

1. No [portal do Azure](https://portal.azure.com/), selecione **Novo** > **Enterprise Integration** > **Gestão de API**.

    Em alternativa, escolha **Novo**, escreva `API management` na caixa de pesquisa e prima Enter. Clique em **Criar**.

2. Na janela **Serviço de Gestão de API**, introduza as definições.

    ![nova instância](./media/get-started-create-service-instance/get-started-create-service-instance-create-new.png)

    | Definição      | Valor sugerido  | Descrição              |
    | ------------ |  ------- | ---------------------------------|
    |**Nome**|Um nome exclusivo para o serviço de Gestão de API| O nome não pode ser alterado mais tarde. O nome do serviço é utilizado para gerar um nome de domínio predefinido na forma de *{nome}.azure-api.net.* Se gostaria de utilizar um nome de domínio personalizado, consulte [Configurar um domínio personalizado](configure-custom-domain.md). <br/> O nome de serviço é utilizado para fazer referência ao serviço e ao recurso do Azure correspondente.|
    |**Subscrição**|A sua subscrição | A subscrição sob a qual esta nova instância do serviço será criada. Pode selecionar a subscrição entre as diferentes subscrições do Azure disponíveis para si.|
    |**Grupo de Recursos**|*apimResourceGroup*|Pode selecionar um recurso novo ou existente. Um grupo de recursos é uma coleção de recursos que partilham o ciclo de vida, as permissões e as políticas. Sabia mais [aqui](../azure-resource-manager/resource-group-overview.md#resource-groups).|
    |**Localização**|*EUA Oeste*|Selecione a região geográfica perto de si. Apenas as regiões de serviço de Gestão de API disponíveis são apresentadas na caixa de lista pendente. |
    |**Nome da organização**|O nome da sua organização|Este nome é utilizado em vários sítios, incluindo o título do portal do programador e o remetente de e-mails de notificação.|
    |**E-mail do administrador**|*admin@org.com*|Defina um endereço de e-mail para o qual serão enviadas todas as notificações da **Gestão de API**.|
    |**Escalão de preço**|*Programador*|Defina o escalão de **Programador** para avaliar o serviço. Este escalão não é para utilização em produção. Para obter mais informações sobre o dimensionamento dos escalões da Gestão de API, consulte [Atualização de versão do software e dimensionamento](upgrade-and-scale.md).|
3. Escolha **Criar**.

    > [!TIP]
    > Normalmente, demora entre 20 e 30 minutos a criar um serviço de Gestão de API. Ao selecionar **Afixar ao dashboard**, é mais fácil localizar um serviço criado recentemente.

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Quando já não for necessário, pode remover o grupo de recursos e todos os recursos relacionados seguindo estes passos:


1. No portal do Azure, selecione ![seta](./media/get-started-create-service-instance/arrow.png).
2. Selecione **Grupos de recursos**.
3. Localize o seu grupo de recursos.
4. Clique em ". . ." e elimine o seu grupo.

![limpeza](./media/get-started-create-service-instance/cleanup.png)

## <a name="next-steps"></a>Passos seguintes

> [!div class="nextstepaction"]
> [Importar e publicar a sua primeira API](import-and-publish.md)
