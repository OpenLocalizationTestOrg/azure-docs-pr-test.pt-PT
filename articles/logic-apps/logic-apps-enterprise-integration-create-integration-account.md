---
title: "aaaCreate, ligar, eliminar ou mover uma conta de integração em aplicações lógicas do Azure | Microsoft Docs"
description: "Como toocreate uma integração conta e ligá-lo tooyour logic apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a>O que é uma conta de integração?

Uma conta de integração permite que aplicações de integração do enterprise toomanage artefactos, incluindo esquemas, mapas, certificados, parceiros e contratos. Qualquer aplicação de integração que criar utiliza um tooaccess de conta de integração estes esquemas, mapas, certificados e assim sucessivamente.

## <a name="create-an-integration-account"></a>Criar uma conta de integração

1.  Inicie sessão no toohello [portal do Azure](http://portal.azure.com "portal do Azure"). No menu à esquerda de Olá, selecione **mais serviços**.

    ![Selecione "Mais serviços"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Na caixa de pesquisa de Olá, escreva "" integração para o filtro. Na lista de resultados de Olá, selecione **contas de automatização**.

    ![Filtrar por "integração", selecione "Contas de automatização"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Em Olá parte superior da página Olá, escolha **adicionar**.

    ![Escolher adicionar](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. A conta de integração e selecione Olá subscrição do Azure que pretende que o toouse de nomes. Pode criar um novo **grupo de recursos** ou selecione um grupo de recursos existente. Em seguida, selecione um **localização** para alojar a sua conta de integração e um **escalão de preço**. 

    Quando estiver pronto, selecione **criar**.

    ![Forneça detalhes para a sua conta de integração](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    Azure Aprovisiona a sua conta de integração na localização de Olá selecionado, o que deve ser concluído dentro de 1 minuto.

5. Atualize a página Olá. Consulte a nova conta de integração listada.

    ![É apresentada a sua nova conta de integração](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

Em seguida, associe a Olá integração conta que é criado tooyour aplicação lógica. 

## <a name="link-an-integration-account-tooa-logic-app"></a>Ligar uma aplicação de lógica de tooa da conta de integração

toogive aceder às suas logic apps toomaps, esquemas, contratos e outros objetos na sua conta de integração, a aplicação de lógica de tooyour integração conta ligação Olá.

### <a name="prerequisites"></a>Pré-requisitos

* Uma conta de integração
* Uma aplicação lógica

> [!NOTE] 
> Certifique-se a aplicação de conta e a lógica de integração Olá *mesma localização do Azure* antes de começar.


1. Olá portal do Azure, selecione a sua aplicação lógica e verifique a localização da sua aplicação lógica.

    ![Selecione a sua aplicação lógica, verifique a localização](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. Em **definições**, selecione **Integration Account**.

    ![Selecione "Conta de integração"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. De Olá **selecionar uma conta de integração** lista, a conta de integração de Olá selecione pretende que a aplicação de lógica de tooyour toolink. toofinish da ligação, escolha **guardar**.

    ![Selecione a sua conta de integração](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    Receberá uma notificação que apresenta a integração de conta é a aplicação de lógica de tooyour ligado e que todos os artefactos na sua conta de integração estão agora disponíveis tooyour aplicação de lógica.

    ![Está ligada a sua aplicação lógica tooyour conta de integração](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

Agora que a sua conta de integração é a aplicação de lógica de tooyour ligado, pode utilizar os conectores de Olá B2B nas suas logic apps. Alguns conectores B2B comuns incluem validação XML e Codificar/descodificar com ficheiros simples.  

## <a name="delete-your-integration-account"></a>Eliminar a conta de integração

1. Selecione **mais serviços**.

    ![Selecione "Mais serviços"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Na caixa de pesquisa de Olá, escreva "" integração para o filtro. Na lista de resultados de Olá, selecione **contas de automatização**.

    ![Filtrar por "integração", selecione "Contas de automatização"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Selecione a conta de integração de Olá que pretende que o toodelete.

    ![Selecione toodelete de conta de integração](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. No menu de Olá, escolha **eliminar**.

    ![Escolha "Eliminar"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. Confirme a sua conta de integração de Olá choice toodelete.

## <a name="move-your-integration-account"></a>Mover a sua conta de integração

toomove um tooanother de conta de integração do Azure subscrição ou grupo de recursos, siga estes passos.

> [!IMPORTANT]
> Tem de atualizar todos os scripts toouse Olá novos IDs de recurso depois de mover uma conta de integração.

1. Selecione **mais serviços**.

    ![Selecione "Mais serviços"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Na caixa de pesquisa de Olá, escreva "" integração para o filtro. Na lista de resultados de Olá, selecione **contas de automatização**.

    ![Filtrar por "integração", selecione "Contas de automatização"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. Selecione a conta de integração de Olá que pretende que o toomove. Em **definições**, escolha **propriedades**.

    ![Selecione toomove de conta de integração. Em definições, escolha Propriedades](./media/logic-apps-enterprise-integration-accounts/move.png)

5. Alterar o grupo de recursos de Olá ou de subscrição do Azure associado à sua conta de integração.

    ![Escolha o grupo de recursos de alteração ou de subscrição de alteração](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a>Passos Seguintes
* [Saiba mais sobre contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre contratos de integração do enterprise")  

