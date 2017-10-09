---
title: "comportamento de aaaOverride HTTP utilizando o motor de regras do Olá CDN do Azure | Microsoft Docs"
description: "o motor de regras de Olá permite-lhe toocustomize como os pedidos de HTTP são processados pela CDN do Azure, tal como está a bloquear Olá entrega de determinados tipos de conteúdo, definir uma política de colocação em cache e modificar os cabeçalhos de HTTP."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a>Substituir o comportamento HTTP utilizando o motor de regras do Olá CDN do Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Descrição geral
o motor de regras de Olá permite-lhe toocustomize como pedidos de HTTP são processados, por exemplo, entrega de Olá de determinados tipos de conteúdo a bloquear, definir uma política de colocação em cache e modificar os cabeçalhos de HTTP.  Este tutorial demonstrar criar uma regra que irá alterar Olá comportamento de ativos CDN a colocação em cache.  Há também conteúdo de vídeo disponível no Olá "[Consulte também](#see-also)" secção.

   > [!TIP] 
   > Para uma sintaxe de toohello de referência em detalhe, consulte [regras motor referência](cdn-rules-engine-reference.md).
   > 


## <a name="tutorial"></a>Tutorial
1. No painel do perfil da CDN Olá, clique em Olá **gerir** botão.
   
    ![Botão de gerir do painel do perfil da CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    portal de gestão de CDN Olá abre.
2. Clique em Olá **HTTP grande** separador, seguido de **motor de regras**.
   
    São apresentadas as opções para uma nova regra.
   
    ![Novas opções de regra CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > ordem de Olá em que várias regras estão listadas afeta a forma como são processadas. Uma regra subsequente pode substituir as ações de Olá especificadas por uma regra de anterior.
   > 
   > 
3. Introduza um nome na Olá **nome / descrição** caixa de texto.
4. Identifique o tipo de Olá de pedidos Olá regra será aplicada a.  Por predefinição, Olá **sempre** está selecionada condição de correspondência.  Irá utilizar **sempre** para este tutorial, por isso deixe que selecionou.
   
   ![Condição de correspondência CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > Existem muitos tipos de correspondência de condições disponíveis no menu pendente de Olá.  Clicar no Olá azul ícone informativa toohello esquerda da condição de correspondência de Olá explicar condição Olá atualmente selecionado em detalhe.
   > 
   >  Para Olá a lista completa de expressões condicionais com detalhes, consulte [expressões condicionais do motor de regras](cdn-rules-engine-reference-match-conditions.md).
   >  
   > Para Olá obter uma lista completa das condições de correspondência em detalhe, consulte [condições de corresponder ao motor de regras](cdn-rules-engine-reference-match-conditions.md).
   > 
   > 
5. Clique em Olá  **+**  no botão seguinte demasiado**funcionalidades** tooadd uma nova funcionalidade.  Na lista pendente de Olá Olá esquerda, selecione **idade de máxima de interno Force**.  Olá caixa de texto que aparece, introduza **300**.  Deixe Olá restantes valores predefinidos.
   
   ![Funcionalidade CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > Como com condições de correspondência, clicando em Olá azul ícone informativa toohello esquerda do Olá nova funcionalidade apresentará detalhes sobre esta funcionalidade.  No caso de Olá de **idade de máxima de interno Force**, iremos são a substituir o recurso de Olá **Cache-Control** e **expira** cabeçalhos toocontrol quando o nó de extremidade CDN Olá atualizará Olá recurso de origem Olá.  Nosso exemplo de 300 segundos significa nó de extremidade CDN Olá irão colocar em cache asset Olá 5 minutos antes de atualizar o recurso de Olá de origem.
   > 
   > Para Olá obter uma lista completa das funcionalidades em detalhe, consulte [detalhes de funcionalidade do motor de regras](cdn-rules-engine-reference-features.md).
   > 
   > 
6. Clique em Olá **adicionar** nova regra do botão toosave Olá.  nova regra de Olá agora está a aguardar aprovação. Quando for aprovado, o estado de Olá deixará de **XML pendente** demasiado**XML Active Directory**.
   
   > [!IMPORTANT]
   > Alterações de regras podem demorar até too90 minutos toopropagate através de Olá CDN.
   > 
   > 

## <a name="see-also"></a>Consultar também
* [Descrição geral da CDN do Azure](cdn-overview.md)
* [Referência do motor de regras](cdn-rules-engine-reference.md)
* [Condições de correspondência do motor de regras](cdn-rules-engine-reference-match-conditions.md)
* [Expressões condicionais de motor de regras](cdn-rules-engine-reference-conditional-expressions.md)
* [Funcionalidades do motor de regras](cdn-rules-engine-reference-features.md)
* [Substituir o comportamento HTTP predefinido utilizando o motor de regras de Olá](cdn-rules-engine.md)
* [Azure sextas: Poderosas novo as funcionalidades Azure CDN Premium](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (vídeo)