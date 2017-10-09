---
title: "aaaHow tooconfigure palavra-passe-início de sessão único para um applicationn não Galeria | Microsoft Docs"
description: "Como tooconfigure uma aplicação não Galeria personalizada para proteger com base em palavra-passe de início de sessão quando não está listado no Olá Galeria de aplicações do Azure AD"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Como a palavra-passe de tooconfigure único início de sessão para uma aplicação não Galeria

Além disso toohello escolhas encontrados Olá do Azure AD Galeria de aplicações, tem também de Olá opção tooadd um **não Galeria aplicação** quando aplicação Olá pretende não estiver indicada não existe. Através desta funcionalidade, pode adicionar qualquer aplicação que já existe na sua organização ou as aplicações de terceiros que poderá utilizar de um fornecedor que já não faz parte de Olá [Galeria de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).

Depois de adicionar uma aplicação não galeria, em seguida, pode configurar Olá único início de sessão método utiliza esta aplicação, selecionando Olá **Single Sign-on** item de navegação numa aplicação empresarial no Olá [Portal do Azure ](https://portal.azure.com/).

Uma das Olá Single Sign-on métodos disponível tooyou é Olá [baseada em palavra-passe Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opção. Com Olá **adicionar uma aplicação não galeria** experiência, pode integrar qualquer aplicação que apresenta um nome de utilizador baseado em HTML e a palavra-passe de entrada no campo, mesmo que não está no nosso conjunto de aplicações previamente integradas.

Isto funciona de forma de Olá é uma página scraping tecnologia que faz parte de Olá extensão do painel de acesso que nos permite tooauto-detetar campos de entrada de nome de utilizador e palavra-passe, armazená-las de forma segura para a instância de aplicação específica. Em seguida, em segurança reprodução de nomes de utilizador e os campos de toothose de palavras-passe quando um utilizador navega toothat aplicação no painel de acesso da aplicação Olá.

Esta é uma excelente forma de tooget iniciado integrar qualquer tipo de aplicação com o Azure AD rapidamente e permite-lhe:

-   Integrar **qualquer aplicação na Olá mundo** com o seu inquilino do Azure AD, por isso, desde compõe um campo de entrada HTML nome de utilizador e palavra-passe

-   Ativar **-início de sessão único para os seus utilizadores** em segurança, armazenar e replaying nomes de utilizador e palavras-passe para a aplicação Olá tiver integrado com o Azure AD

-   **Entrada de deteção automática** campos para qualquer aplicação e permitem-lhe toomanually detetar esses campos utilizando Olá extensão de Browser do painel de acesso, no caso de deteção automática não encontrá-los

-   **Suporta aplicações que necessitam de vários campos de início de sessão** para aplicações que necessitam de mais do que apenas nome de utilizador e palavra-passe campos toosign no

-   **Personalizar etiquetas Olá** dos campos de entrada nome de utilizador e palavra-passe Olá os seus utilizadores verão no Olá [painel de acesso de aplicação](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando ele introduzir as respetivas credenciais

-   Permitir o **utilizadores** tooprovide os seus próprios nomes de utilizador e palavras-passe para as contas de aplicação existentes que são escrever manualmente no Olá [painel de acesso de aplicação](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   Permitir que um **membro do grupo de empresas Olá** nomes de utilizador do toospecify Olá e palavras-passe tooa utilizador atribuído utilizando Olá [Self-Service de acesso de aplicação](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) funcionalidade

-   Permitir que um **administrador** nomes de utilizador do toospecify Olá e palavras-passe atribuídas tooa utilizador com credenciais de atualização de Olá funcionalidade quando [atribuir uma aplicação de tooan do utilizador](#_How_to_configure_1)

-   Permitir que um **administrador** funcionalidade quando o nome de utilizador do toospecify Olá partilhado ou palavra-passe utilizada por um grupo de pessoas com as credenciais de atualização de Olá [atribuir uma aplicação de tooan de grupo](#assign-an-application-to-a-group-directly)

A seguir descreve como pode permitir [baseada em palavra-passe Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) aplicação tooany adicionar utilizando Olá **adicionar uma aplicação não galeria** experiência.

## <a name="overview-of-steps-required"></a>Descrição geral dos passos necessários

tooconfigure uma aplicação na galeria do Azure AD de Olá tem de:

-   [Adicionar uma aplicação não Galeria](#add-a-non-gallery-application)

-   [Configurar aplicação Olá para palavra-passe-início de sessão único](#configure-the-application-for-password-single-sign-on)

-   [Atribuir Olá aplicação tooa utilizador ou um grupo](#assign-the-application-to-a-user-or-a-group)

    -   [Atribuir diretamente uma aplicação de tooan do utilizador](#assign-a-user-to-an-application-directly)

    -   [Atribuir diretamente o grupo de tooa uma aplicação](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a>Adicionar uma aplicação não Galeria

tooadd uma aplicação Olá Galeria AD do Azure, siga os passos de Olá abaixo:

1.  Abra Olá [Portal do Azure](https://portal.azure.com) e inicie sessão como um **Administrador Global** ou **coadministrador**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em Olá **adicionar** botão no canto superior direito de Olá no Olá **aplicações empresariais** painel

6.  Clique em **aplicação não galeria.**

7.  Introduza o nome de Olá da sua aplicação no Olá **nome** caixa de texto. Selecione **adicionar.**

Após um curto período de tempo, ser painel de configuração da aplicação Olá toosee possível.

## <a name="configure-hello-application-for-password-single-sign-on"></a>Configurar aplicação Olá para palavra-passe-início de sessão único

tooconfigure-início de sessão único para uma aplicação, siga os passos de Olá abaixo:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.

  * Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**

6.  Selecione aplicação Olá pretende tooconfigure-início de sessão único.

7.  Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.

8.  Modo de Olá selecione **baseada em palavra-passe de início de sessão.**

9.  Introduza Olá **URL de início de sessão**. Este é o URL de olá onde os utilizadores introduzem as respetivas toosign no nome de utilizador e palavra-passe para. Certifique-se de que o início de sessão Olá nos campos está visíveis no URL Olá.

10. Atribua utilizadores toohello aplicação.

11. Além disso, também pode fornecer as credenciais em nome de utilizador de Olá, selecionar linhas Olá de utilizadores de Olá e clicando na **credenciais de atualização** e introduzindo Olá nome de utilizador e palavra-passe em nome dos utilizadores de Olá. Caso contrário, os utilizadores ser tooenter pedido Olá credenciais próprios após iniciar.

## <a name="assign-a-user-tooan-application-directly"></a>Atribuir diretamente uma aplicação de tooan do utilizador

tooassign um ou mais aplicações de tooan utilizadores diretamente, siga os passos de Olá abaixo:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.

  * Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**

6.  Selecione aplicação Olá pretende tooassign uma lista de Olá de toofrom do utilizador.

7.  Quando carrega a aplicação Olá, clique em **utilizadores e grupos** do menu de navegação esquerdo da aplicação Olá.

8.  Clique em Olá **adicionar** botão por cima Olá **utilizadores e grupos** Olá de tooopen lista **adicionar atribuição** painel.

9.  Clique em Olá **utilizadores e grupos** Seletor de Olá **adicionar atribuição** painel.

10. Tipo de Olá **nome completo** ou **endereço de correio eletrónico** do utilizador Olá estiver interessado em atribuir para Olá **pesquisa por nome ou endereço de e-mail** caixa de pesquisa.

11. Coloque o cursor sobre Olá **utilizador** no Olá lista tooreveal um **caixa de verificação**. Clique em tooadd de fotografias ou logótipo do perfil do Olá caixa de verificação seguinte toohello utilizador seu utilizador toohello **selecionados** lista.

12. **Opcional:** se gostaria demasiado**adicionar mais do que um utilizador**, tipo noutra **nome completo** ou **endereço de correio eletrónico** para Olá **pesquisar por nome ou o endereço de correio eletrónico** caixa de pesquisa e clique em Olá caixa de verificação tooadd toohello este utilizador **selecionados** lista.

13. Quando tiver terminado de selecionar utilizadores, clique em Olá **selecione** botão tooadd-los toohello lista de utilizadores e grupos toobe atribuído toohello aplicação.

14. **Opcional:** clique Olá **selecionar função** Seletor no Olá **adicionar atribuição** painel tooselect uma função tooassign toohello utilizadores que selecionou.

15. Clique em Olá **atribuir** botão tooassign Olá aplicação toohello utilizadores selecionados.

## <a name="assign-an-application-tooa-group-directly"></a>Atribuir diretamente o grupo de tooa uma aplicação

tooassign um ou mais grupos de aplicações de tooan diretamente, siga Olá passos abaixo:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.

  * Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**

6.  Selecione aplicação Olá pretende tooassign uma lista de Olá de toofrom do utilizador.

7.  Quando carrega a aplicação Olá, clique em **utilizadores e grupos** do menu de navegação esquerdo da aplicação Olá.

8.  Clique em Olá **adicionar** botão por cima Olá **utilizadores e grupos** Olá de tooopen lista **adicionar atribuição** painel.

9.  Clique em Olá **utilizadores e grupos** Seletor de Olá **adicionar atribuição** painel.

10. Tipo de Olá **nome do grupo completa** do grupo de Olá estiver interessado em atribuir para Olá **pesquisa por nome ou endereço de e-mail** caixa de pesquisa.

11. Coloque o cursor sobre Olá **grupo** no Olá lista tooreveal um **caixa de verificação**. Clique em tooadd de fotografias ou logótipo do perfil do Olá caixa de verificação seguinte toohello grupo seu utilizador toohello **selecionados** lista.

12. **Opcional:** se gostaria demasiado**adicionar mais de um grupo**, tipo noutra **nome do grupo completo de** para Olá **pesquisa por nome ou endereço de e-mail** caixa de pesquisa e clique em Olá caixa de verificação tooadd toohello este grupo **selecionados** lista.

13. Quando tiver terminado de selecionar grupos, clique em Olá **selecione** botão tooadd-los toohello lista de utilizadores e grupos toobe atribuído toohello aplicação.

14. **Opcional:** clique Olá **selecionar função** Seletor no Olá **adicionar atribuição** painel tooselect toohello de tooassign uma função de grupos selecionou.

15. Clique em Olá **atribuir** botão tooassign Olá aplicação toohello grupos selecionados.

Após um curto período de tempo, os utilizadores Olá que selecionou ser capaz de toolaunch estas aplicações em Olá painel de acesso.

## <a name="next-steps"></a>Passos seguintes
[Fornecer aplicações de tooyour de início de sessão único com o Proxy da aplicação](active-directory-application-proxy-sso-using-kcd.md)
