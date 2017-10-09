---
title: "acesso de aplicação personalizada aaaHow toouse | Microsoft Docs"
description: "Ativar o acesso de aplicação personalizada tooallow toofind de utilizadores as suas próprias aplicações"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a>Como aceder a aplicações de self-service toouse

Antes dos utilizadores Self-podem detetar as aplicações a partir do respetivo painel de acesso, terá de tooenable **acesso à aplicação self-service** aplicações tooany pretende tooallow utilizadores tooself-detetar e pedir acesso para.

Esta funcionalidade é uma excelente forma de toosave tempo e dinheiro como um grupo de TI e é altamente recomendada como parte de uma implementação de aplicações modernas com o Azure Active Directory.

Utilizar esta funcionalidade, pode:

-   Permitir que os utilizadores Self-detetar as aplicações de Olá [painel de acesso de aplicação](https://myapps.microsoft.com/) sem bothering Olá IT grupo.

-   Adicione esses grupo de pré-configurado de tooa de utilizadores para que possa ver quem tiver solicitado acesso, remover o acesso e gerir funções de Olá atribuídas toothem.

-   Opcionalmente, permitir que um aprovador empresarial pedidos de acesso de aplicação tooapprove pelo Olá grupo TI não tem.

-   Opcionalmente, configure cópias de segurança too10 se a indivíduos que podem aprovar acesso toothis aplicação.

-   Opcionalmente, permitir que um aprovador empresarial palavras-passe do tooset Olá esses utilizadores podem utilizar toosign na aplicação toohello, diretamente a partir do aprovador de negócio a Olá [painel de acesso de aplicação](https://myapps.microsoft.com/).

-   Opcionalmente, automaticamente diretamente a atribuir a função de aplicação de tooan de utilizadores atribuídos self-service.

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a>Ativar o acesso de aplicação personalizada tooallow toofind de utilizadores as suas próprias aplicações

Acesso de aplicação personalizada é tooself de utilizadores de tooallow uma excelente forma-detetar aplicações, opcionalmente, permitir Olá negócio tooapprove acesso grupo toothose aplicações. Pode permitir que as credenciais grupo Olá negócio toomanage Olá atribuído toothose utilizadores para a direita da palavra-passe de início de sessão único em aplicações da respetiva painéis de acesso.

aplicação de tooan de acesso por aplicação self-service tooenable, siga Olá passos abaixo:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.

  * Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**

6.  Selecione aplicação Olá pretende tooenable self-service access toofrom Olá List, lista.

7.  Quando carrega a aplicação Olá, clique em **self-service** do menu de navegação esquerdo da aplicação Olá.

8.  tooenable acesso a aplicações de self-service para esta aplicação, ative Olá **permitir que os utilizadores a aplicação do toorequest acesso toothis?** alternar demasiado**Sim.**

9.  Em seguida, tooselect Olá grupo toowhich os utilizadores que pedem acesso toothis aplicações devem ser adicionadas, clique em etiqueta de toohello seguinte Seletor Olá **toowhich grupo deve ser atribuído aos utilizadores adicionar?** e selecione um grupo.

10. **Opcional:** se quiser toorequire uma aprovação de negócio antes dos utilizadores têm permissão de acesso, defina Olá **exigir a aprovação antes de conceder acesso toothis aplicação?** alternar demasiado**Sim**.

11. **Opcional: para aplicações utilizando a palavra-passe início de sessão único em apenas,** se desejar tooallow essas empresas aprovadores toospecify Olá palavras-passe que são enviadas toothis aplicação para os utilizadores aprovados, defina Olá **permitir aprovadores tooset palavras-passe do utilizador para esta aplicação?**  alternar demasiado**Sim**.

12. **Opcional:** aprovadores de negócio de Olá toospecify autorizados tooapprove aplicação de toothis de acesso, clique em etiqueta de toohello seguinte Seletor Olá **que é permitida a aplicação do tooapprove acesso toothis?** tooselect cópias de segurança too10 aprovadores de negócio individuais.

   * Não são suportados grupos.

13. **Opcional:** **para aplicações que expõem funções**, se assim o desejar a função de tooa do tooassign utilizadores aprovados self-service, clique em Olá Seletor seguinte toohello **toowhich função devem ser atribuído aos utilizadores deste aplicação?**  tooselect Olá função toowhich devem ser atribuídos estes utilizadores.

14. Clique em Olá **guardar** botão, Olá parte superior do Olá painel toofinish.

Depois de concluir a configuração da aplicação de self-service, os utilizadores podem navegar tootheir [painel de acesso de aplicação](https://myapps.microsoft.com/) e clique em Olá **+ adicionar** botão toofind Olá aplicações toowhich tiver ativado Acesso de self-service. Aprovadores negócio também veem uma notificação no respetivo [painel de acesso de aplicação](https://myapps.microsoft.com/). Pode ativar uma mensagem de e-mail a indicar quando um utilizador pediu a aplicação de tooan de acesso que requer a sua aprovação. 

Estas aprovações suportam aprovação único fluxos de trabalho apenas, que significa que, se especificar vários aprovadores, qualquer aprovador único pode aprovar acesso toohello aplicação.

## <a name="next-steps"></a>Passos seguintes
[Configurar o Azure Active Directory para gestão de grupos self-service](active-directory-accessmanagement-self-service-group-management.md)
