---
title: "aaaProblems tooan configurada para a palavra-passe de aplicação de galeria do Azure AD de início de sessão de sessão único-| Microsoft Docs"
description: "Aborda áreas problemáticas que fornecem orientações tootroubleshoot emite toosigning relacionado no tooAzure aplicações Galeria AD configuradas para a palavra-passe-início de sessão único"
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
ms.openlocfilehash: f53ef4176db37dc6b1da2d61027155a6ba8f331e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-password-single-sign-on"></a>Problemas em iniciar sessão tooan configurada para a palavra-passe-início de sessão único de aplicação de galeria do Azure AD

Olá painel de acesso é um portal baseado na web que permitem que um utilizador que possua uma empresa ou escola da conta do Azure Active Directory (Azure AD) tooview e inicie baseado na nuvem aplicações esse administrador Olá do Azure AD concedeu-lhes acesso. Um utilizador que possua as edições do Azure AD também pode utilizar grupos self-service e capacidades de gestão de aplicações através de Olá painel de acesso. Olá painel de acesso separado do Olá portal do Azure e não necessita que os utilizadores toohave uma subscrição do Azure.

toouse baseada em palavra-passe-início de sessão único (SSO) no painel de acesso, Olá extensão do painel de acesso de Olá tem de estar instalado no browser do utilizador Olá. Esta extensão é transferida automaticamente quando um utilizador seleciona uma aplicação que está configurada para SSO baseada em palavra-passe.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Que cumprem os requisitos de browser para Olá painel de acesso

Olá painel de acesso necessita de um browser que suporte JavaScript e ativou CSS. toouse baseada em palavra-passe-início de sessão único (SSO) no painel de acesso, Olá extensão do painel de acesso de Olá tem de estar instalado no browser do utilizador Olá. Esta extensão é transferida automaticamente quando um utilizador seleciona uma aplicação que está configurada para SSO baseada em palavra-passe.

Para SSO baseada em palavra-passe, podem ser browsers do utilizador final Olá:

-   Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior

-   Chrome – No Windows 7 ou posterior e no MacOS X ou posterior

-   Firefox 26.0 ou posterior – no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior

>[!NOTE]
>extensão SSO baseada em palavra-passe Olá fiquem disponíveis para Edge no Windows 10 quando as extensões de browser ficarem suportadas para o limite.
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Como tooinstall Olá extensão de Browser do painel de acesso

Olá tooinstall extensão de Browser do painel de acesso, siga os passos de Olá abaixo:

1.  Abra Olá [painel de acesso](https://myapps.microsoft.com) dos browsers Olá suportado e inicie sessão como um **utilizador** no seu Azure AD.

2.  Clique num **aplicação de palavra-passe SSO** no Olá painel de acesso.

3.  Olá prompt perguntar tooinstall Olá software, selecione **instalar agora**.

4.  Com base no seu browser ser toohello direcionados hiperligação de transferência. **Adicionar** browser de tooyour Olá extensão.

5.  Se o browser pede-lhe, selecione tooeither **ativar** ou **permitir** Olá extensão.

6.  Uma vez instalado, **reiniciar** a sessão do browser.

7.  Inicie sessão no painel de acesso de Olá e veja se pode **iniciar** as aplicações de SSO de palavra-passe

Também pode transferir a extensão de Olá para Chrome e Firefox de hiperligações diretas Olá abaixo:

-   [Extensão de painel de acesso do Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extensão de painel de acesso de Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Configurar uma política de grupo para o Internet Explorer

Pode configurar uma política de grupo que lhe permitem extensão do tooremotely instalação Olá painel de acesso para o Internet Explorer em máquinas dos seus utilizadores.

Pré-requisitos de Olá incluem:

-   Configurou [serviços de domínio do Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), e associar domínio de tooyour de máquinas dos seus utilizadores.

-   Tem de ter Olá "Editar as definições" permissão tooedit Olá objeto de política de grupo (GPO). Por predefinição, os membros Olá seguintes grupos de segurança têm esta permissão: os administradores do domínio, administradores da empresa e proprietários de criador de política de grupo. [Saiba mais](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Siga o tutorial Olá [como tooDeploy Olá a extensão do painel de acesso para o Internet Explorer utilizando a política de grupo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) para instruções passo a passo sobre como tooconfigure Olá política de grupo e implementá-la toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Resolver problemas de Olá painel de acesso no Internet Explorer

Siga Olá [Olá de resolução de problemas extensão do painel de acesso para o Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guia para acesso de uma ferramenta de diagnóstico e instruções passo a passo sobre como configurar a extensão de Olá de i/e.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Como a palavra-passe de tooconfigure único início de sessão para uma aplicação não Galeria

tooconfigure uma aplicação na galeria do Azure AD de Olá tem de:

-   [Adicionar uma aplicação não Galeria](#add-a-non-gallery-application)

-   [Configurar aplicação Olá para palavra-passe-início de sessão único](#configure-the-application-for-password-single-sign-on)

-   [Atribuir utilizadores toohello aplicação](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a>Adicionar uma aplicação não Galeria

tooadd uma aplicação Olá Galeria AD do Azure, siga os passos de Olá abaixo:

1.  Abra Olá [Portal do Azure](https://portal.azure.com) e inicie sessão como um **Administrador Global** ou **coadministrador**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em Olá **adicionar** botão no canto superior direito de Olá no Olá **aplicações empresariais** painel

6.  Clique em **aplicação não galeria.**

7.  Introduza o nome de Olá da sua aplicação no Olá **nome** caixa de texto. Selecione **adicionar.**

Após um curto período de tempo, ser painel de configuração da aplicação Olá toosee possível.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurar aplicação Olá para palavra-passe-início de sessão único

tooconfigure-início de sessão único para uma aplicação, siga os passos de Olá abaixo:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.

   * Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**

6.  Selecionar aplicação Olá pretende tooconfigure-início de sessão único

7.  Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.

8.  Modo de Olá selecione **baseada em palavra-passe de início de sessão.**

9.  Introduza Olá **URL de início de sessão**. Este é o URL de olá onde os utilizadores introduzem as respetivas toosign no nome de utilizador e palavra-passe para. Certifique-se de que o início de sessão Olá nos campos está visíveis no URL Olá.

10. Atribua utilizadores toohello aplicação.

11. Além disso, também pode fornecer as credenciais em nome de utilizador de Olá, selecionar linhas Olá de utilizadores de Olá e clicando na **credenciais de atualização** e introduzindo Olá nome de utilizador e palavra-passe em nome dos utilizadores de Olá. Caso contrário, os utilizadores ser tooenter pedido Olá credenciais próprios após iniciar.

### <a name="assign-users-toohello-application"></a>Atribuir utilizadores toohello aplicação

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

Após um curto período de tempo, os utilizadores Olá que selecionou ser capaz de toolaunch estas aplicações em Olá painel de acesso.

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Se estes passos de resolução de problemas não Olá resolver o problema de Olá

Abra um pedido de suporte com Olá se disponíveis os seguintes informações:

-   ID de correlação de erro

-   UPN (endereço de e-mail do utilizador)

-   TenantID

-   Tipo de browser

-   Fuso horário e tempo/período de tempo durante o erro ocorre

-   Rastreios de fiddler

## <a name="next-steps"></a>Passos seguintes
[Fornecer aplicações de tooyour de início de sessão único com o Proxy da aplicação](active-directory-application-proxy-sso-using-kcd.md)

