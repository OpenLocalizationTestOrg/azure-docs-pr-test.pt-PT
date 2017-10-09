---
title: "aplicações de aaaHow aparecem no painel de acesso de Olá | Microsoft Docs"
description: "Resolver problemas com a razão pela qual uma aplicação é apresentados no painel de acesso de Olá"
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
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a>Como as aplicações são apresentadas no painel de acesso de Olá

Olá painel de acesso é um portal baseado na web que permite que um utilizador com um trabalho ou conta de escolares no Azure Active Directory (Azure AD) tooview início baseado na nuvem aplicações e esse Olá administrador do Azure AD concedeu-lhes acesso a. Estas aplicações estão configuradas em nome de utilizador de Olá no portal do Azure AD Olá. Olá, admin pode aprovisionar utilizador de Olá aplicação toohello diretamente ou grupo tooa que um utilizador faz parte de resultando na aplicação Olá, volte a aparecer no painel de acesso do utilizador Olá.

## <a name="general-issues-toocheck-first"></a>Geral emite toocheck pela primeira vez

-   Se uma aplicação apenas foi removida de um utilizador ou grupo Olá utilizador seja um membro, tente toosign e terminar novamente no painel de acesso do utilizador Olá após alguns minutos toosee se Olá aplicação for removida.

-   Se uma licença apenas tiver sido removida de um utilizador ou o utilizador de Olá de grupo é que um membro deste processo poderá demorar muito tempo, dependendo do tamanho de Olá e complexidade do grupo Olá toobe as alterações efetuada. Permitir tempo adicional antes de iniciar sessão Olá painel de acesso.

## <a name="problems-related-tooassigning-applications-toousers"></a>Problemas relacionados tooassigning aplicações toousers

Um utilizador pode estar a ver uma aplicação no respetivo painel de acesso porque estes tinham sido anteriormente atribuídos tooit. Seguem-se algumas toocheck formas:

-   [Certifique-se um utilizador atribuído toohello aplicação](#check-if-a-user-is-assigned-to-the-application)

-   [Verifique se um utilizador com uma licença relacionada com a aplicação de toohello](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a>Certifique-se um utilizador atribuído toohello aplicação

toocheck se um utilizador for atribuído toohello aplicação, siga os passos de Olá abaixo:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.

6.  **Pesquisa** Olá nome da aplicação Olá em questão.

7.  Clique em **utilizadores e grupos**.

8.  Verifique toosee se o utilizador está atribuído toohello aplicação.

  * Se pretender que o utilizador de Olá tooremove da aplicação Olá, **clique Olá linha** do utilizador Olá e selecione **eliminar**.

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Verifique se um utilizador com uma licença relacionada com a aplicação de toohello

toocheck um utilizador atribuído licenças, siga Olá passos abaixo:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **utilizadores e grupos** no menu de navegação de Olá.

5.  Clique em **todos os utilizadores**.

6.  **Pesquisa** para utilizador Olá que está interessado e **clique Olá linha** tooselect.

7.  Clique em **licenças** toosee que licenças Olá atualmente atribuída utilizador.

   * Se o utilizador Olá está atribuído a licença do Office tooan isto ativar tooappear de aplicações do Office de terceiros primeiro no Olá painel de acesso do utilizador.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Problemas relacionados tooassigning aplicações toogroups

Um utilizador pode estar a ver uma aplicação no respetivo painel de acesso porque fazem parte de um grupo que tenha sido atribuído aplicação Olá. Seguem-se algumas toocheck formas:

-   [Verifique as associações de grupo do utilizador](#check-a-users-group-memberships)

-   [Verifique se um utilizador for um membro de um grupo atribuído tooa licença](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a>Verifique as associações de grupo do utilizador

toocheck associação a um grupo, siga Olá passos abaixo:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **utilizadores e grupos** no menu de navegação de Olá.

5.  Clique em **todos os utilizadores**.

6.  **Pesquisa** para utilizador Olá que está interessado e **clique Olá linha** tooselect.

7.  Clique em **grupos.**

8.  Verifique toosee se o utilizador for parte de uma aplicação de toohello do grupo atribuído.

   * Se pretender que o utilizador de Olá tooremove do grupo de Olá **clique Olá linha** do grupo de Olá e selecione eliminar.

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a>Verifique se um utilizador for um membro de um grupo atribuído tooa licença

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **utilizadores e grupos** no menu de navegação de Olá.

5.  Clique em **todos os utilizadores**.

6.  **Pesquisa** para utilizador Olá que está interessado e **clique Olá linha** tooselect.

7.  Clique em **grupos.**

8.  Clique em linha Olá de um grupo específico.

9.  Clique em **licenças** toosee tooit atribuído com o grupo de Olá de licenças.

  * Se o grupo de Olá está atribuído a licença do Office tooan que isto poderá ativar determinada tooappear de aplicações do Office de terceiros primeiro no Olá painel de acesso do utilizador.


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Se estes passos de resolução de problemas não Olá resolver o problema de Olá

Abra um pedido de suporte com Olá se disponíveis os seguintes informações:

-   ID de correlação de erro

-   UPN (endereço de e-mail do utilizador)

-   ID do inquilino

-   Tipo de browser

-   Fuso horário e tempo/período de tempo durante o erro ocorre

-   Rastreios de fiddler

## <a name="next-steps"></a>Passos seguintes
[Gestão de aplicações com o Azure Active Directory](active-directory-enable-sso-scenario.md)
