---
title: "aaaWhat é o painel de acesso de Olá no Azure Active Directory? | Microsoft Docs"
description: "Saiba como toouse variações de Olá aceder ao painel (web browser, aplicação Android, as aplicações de iPhone e iPad) tooaccess aplicações SaaS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 800be6a69f13978c5b88e2fe28a416d4b763656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-access-panel"></a>O que é o painel de acesso de Olá?

Painel de acesso de Olá é um portal baseado na web. Permite que um utilizador com um trabalho ou aceder a conta da escola no Azure Active Directory tooview início baseado na nuvem aplicações e um administrador do Azure AD concedeu-los para. Também pode utilizar grupos self-service e capacidades de gestão de aplicações através do painel de acesso de Olá.

Painel de acesso de Olá está separado do Olá portal do Azure e faz a não lhe toohave uma subscrição do Azure.

![Painel de Acesso][1]

Painel de acesso de Olá permite-lhe tooedit Olá algumas das suas definições de perfil, incluindo a capacidade para:

- Alterar Olá palavra-passe associada a uma conta escolar ou profissional

- Editar definições de reposição de palavra-passe

- Editar contacte e autenticação de fator de toomulti relacionados de definições de preferência (para contas que foram toouse necessária-lo por um administrador)

- Ver detalhes, tais como o ID de utilizador, alternativa dispositivos e mobile e office números de telefone e e-mail, de conta

- Ver e iniciar baseado na nuvem das aplicações que Olá administrador do Azure AD concedeu-lhes acesso a. Para obter mais informações sobre o painel de acesso de Olá perspetiva dos utilizadores Olá, ver a utilizar o painel de acesso de Olá. 

- Self-gerir grupos. Mais especificamente, o administrador de Olá pode criar e gerir grupos de segurança e as associações de grupo de segurança de pedido no Azure AD. Para obter mais informações, consulte [gestão de grupos self-service para utilizadores no Azure AD](active-directory-accessmanagement-self-service-group-management.md) e [gerir os grupos](active-directory-manage-groups.md).




## <a name="accessing-hello-access-panel"></a>Aceder ao painel de acesso de Olá

Pode aceder ao painel de acesso de Olá, visitando Olá os seguintes URL num browser:`http://myapps.microsoft.com`

Se tiver personalizado uma imagem corporativa configurado para a sua página de início de sessão, pode carregar esta imagem corporativa, acrescentando domínio toohello final da sua organização Olá URL:`http://myapps.microsoft.com/<your domain>.com`

Neste caso, pode utilizar qualquer nome de domínio do Active Directory ou verificado que tenha sido configurado no portal do Azure.

![Nome de domínio do Wingtip Toys][2]  

É necessário toodistribute Olá URL tooall os utilizadores que irão iniciar sessão tooapplications que estão integradas com o Azure AD.

## <a name="authentication"></a>Autenticação

Painel de acesso do tooreach Olá, tem de ser autenticado através de uma conta escolar ou profissional no Azure AD. Pode ser autenticado tooAzure AD diretamente. Em alternativa, se uma organização tiver configurado a Federação ao utilizar serviços de Federação do Active Directory (AD FS) ou outras tecnologias, pode ser autenticada pelo Windows Server Active Directory.

Se tiver uma subscrição do Azure ou do Office 365 e utiliza o Olá portal do Azure ou uma aplicação do Office 365, pode ver a lista de Olá das aplicações sem iniciar sessão novamente. Se não são autenticados são toosign pedido no utilizando Olá nome de utilizador e palavra-passe para a sua conta no Azure AD. Se a sua organização tiver configurado a Federação, escrever o nome de utilizador Olá é suficiente.

Quando são autenticados, pode interagir com aplicações de Olá que o administrador tem integrado com o diretório de Olá. toolearn como toointegrate aplicações com o Azure AD, consulte [que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="web-browser-requirements"></a>Requisitos de Web browsers

No mínimo, o painel de acesso de Olá requer um browser que suporte JavaScript e ativou CSS. Para Olá toobe de utilizador com sessão iniciada tooapplications através de com base em palavra-passe-início de sessão único (SSO), a extensão de painel de acesso de Olá tem de estar instalado no seu browser. extensão de Olá é transferida automaticamente quando seleciona uma aplicação que está configurada para SSO baseada em palavra-passe.

extensão de painel de acesso de Olá está atualmente disponível para o Internet Explorer 8 e posteriores, limite, o Chrome e o Firefox browsers.

## <a name="mobile-app-support"></a>Suporte de aplicações móveis

equipa do Azure Active Directory Olá publica Olá minha aplicação móvel de aplicações. Quando instalar aplicação Olá, pode iniciar sessão com base em toopassword SSO as aplicações em dispositivos iOS e Android.

> [!NOTE]
> Pode iniciar sessão tooapplications que suporta a Federação com o Azure AD (incluindo o Salesforce, Google Apps, Dropbox, caixa, Concur, Workday, Office 365 e 70 mais do que outras pessoas) em praticamente qualquer browser web, em qualquer dispositivo, sem necessitar de uma aplicação de plug-in ou móvel. Todos os outros [experiências do painel de acesso](https://myapps.microsoft.com/) não também necessitam de Olá toobe de aplicação móvel minhas aplicações utilizado num dispositivo móvel.
>
>

### <a name="my-apps-for-android"></a>Minhas aplicações para Android

As minhas aplicações para Android é suportada em qualquer dispositivo Android que está a executar a versão Android 4.1 e posterior.  
Está disponível no Olá [loja do Google Play](https://play.google.com/store/apps/details?id=com.microsoft.myapps).

![Minhas aplicações para Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a>Minhas aplicações para iPhone e iPad

As minhas aplicações para iOS é suportada em qualquer iPhone ou iPad, que está a executar a versão do iOS 7 e posterior.  
Está disponível no Olá [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).

![Minhas aplicações para iOS][4]    



## <a name="managed-browser-for-my-apps"></a>Browser gerido para as minhas aplicações

As minhas aplicações também está integrado em Olá Browser gerido do Intune. Olá Browser gerido do Intune para dispositivos iOS e Android desempenha um papel chave garantir que permanecem proteger dados em dispositivos móveis. Permite-lhe possam ver e navegue páginas web que poderão conter informações da empresa e fornece uma experiência de navegação na web segura.  
Encontrará acesso rápido toomy aplicações na sua home page de Browser gerido e no seu marcadores, dando-lhe menos clica tooreach qualquer aplicação que pretende tooaccess.

Está disponível no Olá [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) e [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

![Browser Mananged para as minhas aplicações][5]    





## <a name="tips-for-testing-hello-user-experience"></a>Sugestões para uma experiência de utilizador Olá teste

Se for um administrador do Azure e tem sessão iniciada toohello portal do Azure, utilizando uma conta no diretório de Olá, automaticamente iniciada no painel de acesso de toohello como a sua conta atual. Neste caso, pode ver todas as aplicações que tenham sido atribuídas tooyou.

**tootest como um *diferentes* conta de utilizador:**

1. Clique Olá menu de utilizador no canto superior direito de Olá de Olá portal do Azure ou do painel de acesso de Olá e, em seguida, selecione **terminar sessão**. 
2. Aceda toohello [painel de acesso](http://myapps.microsoft.com).
3. Na página de início de sessão Olá, o nome de utilizador do tipo Olá e palavra-passe da conta de Olá no seu diretório quiser tootest.


## <a name="starting-applications"></a>Início de aplicações

Vários tipos de aplicações podem aparecer no painel de acesso de Olá.

### <a name="office-365-applications"></a>Aplicações do Office 365

Se a sua organização está a utilizar aplicações do Office 365 e está licenciado para os mesmos, aplicações de Olá do Office 365 aparecem no painel de acesso.

Ao clicar um mosaico de aplicação para uma aplicação do Office 365, é redirecionada toohello aplicação e automaticamente com sessão iniciada.

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a>Aplicações de terceiros da Microsoft e configuradas com o SSO baseada em Federação

O administrador pode adicionar aplicações Olá secção Olá portal do Azure Active Directory com o modo SSO Olá definido demasiado**do Azure AD Single Sign-On**. Só pode ver estas aplicações, se o administrador tem explicitamente concedidos que acesso toohello aplicações.

Ao clicar num mosaico para uma destas aplicações, são redirecionados e sessão na aplicação toohello será iniciada automaticamente.

### <a name="password-based-sso-without-identity-provisioning"></a>SSO baseada em palavra-passe sem aprovisionamento de identidade

O administrador pode adicionar aplicações Olá secção Olá portal do Azure Active Directory com o modo SSO Olá definido demasiado**baseada em palavra-passe Single Sign-On**. Todos os utilizadores no diretório de Olá podem ver todas as aplicações que tenham sido configuradas neste modo.

Olá pela primeira vez, clicar num mosaico para uma destas aplicações, são tooinstall pedido Olá SSO de palavra-passe Plug-in para o Internet Explorer ou o Chrome. instalação de Olá exijam toorestart o web browser. Quando devolver toohello painel de acesso e clique no mosaico aplicações Olá novamente, lhe for pedido um nome de utilizador e palavra-passe da aplicação Olá. Quando introduzir o nome de utilizador e palavra-passe, estas credenciais são armazenadas de forma segura e ligado tooyour conta no Azure AD.

Olá próxima vez que clicar em mosaico de aplicação Olá, automaticamente iniciada toohello aplicação.  
Não tem tooenter as suas credenciais novamente e ou instalar Olá Plug-in de SSO de palavra-passe.

Se tem alterado as suas credenciais na aplicação de terceiros de destino Olá, tem também de atualizar as suas credenciais são armazenadas no Azure AD. 

**tooupdate credenciais:**

1. Selecione o ícone de Olá no mosaico de aplicação Olá.
2. Selecione **atualizar credenciais** Olá, o nome de utilizador do tooreenter Olá e a palavra-passe da aplicação.


### <a name="password-based-sso-with-identity-provisioning"></a>SSO baseada em palavra-passe com o aprovisionamento de identidade

O administrador pode adicionar aplicações no Olá **do Active Directory** secção Olá portal do Azure com o modo SSO Olá definido demasiado**baseada em palavra-passe Single Sign-On**, juntamente com o aprovisionamento de identidade.

Olá pela primeira vez, clicar num mosaico de aplicação para uma destas aplicações, são tooinstall pedido Olá **SSO de palavra-passe Plug-in para o Internet Explorer ou o Chrome**. instalação de Olá exijam toorestart o web browser.  
Quando devolver toohello painel de acesso e clique no mosaico aplicações Olá novamente iniciada automaticamente na aplicação toohello.

Algumas aplicações podem requerer toochange a sua palavra-passe Olá primeiro início de sessão. Se tem alterado as suas credenciais na aplicação de terceiros de destino Olá, tem também de atualizar as credenciais de Olá que estão armazenadas no Azure AD. 

**tooupdate credenciais:**

1. Selecione o ícone de Olá no mosaico de aplicação Olá.
2. Selecione **atualizar credenciais** Olá, o nome de utilizador do tooreenter Olá e a palavra-passe da aplicação.


### <a name="application-with-existing-sso-solutions"></a>Aplicações com soluções de SSO existentes

tooconfigure SSO para uma aplicação, Olá portal do Azure fornece uma terceira opção, denominada **existente Single Sign-On**. Esta opção permite toocreate seu administrador uma aplicação de tooan de ligação e coloque-a no painel de acesso de Olá para utilizadores selecionados.

Por exemplo, se uma aplicação é configurada tooauthenticate utilizadores através do AD FS 2.0, o administrador pode utilizar Olá **existente Single Sign-On** opção toocreate tooit uma ligação no painel de acesso de Olá. Ao aceder a ligação de Olá, são autenticadas através do AD FS 2.0 ou fornece de qualquer aplicação Olá de solução SSO existente.


## <a name="next-steps"></a>Passos seguintes

- toosee uma lista de todos os tópicos que estão relacionados tooapplication gestão, consulte Olá [índice de artigos da gestão de aplicações no Azure Active Directory](active-directory-apps-index.md).
 
- toolearn como toointegrate uma aplicação SaaS com o Azure AD, consulte Olá [lista de tutoriais sobre como aplicações de SaaS toointegrate](active-directory-saas-tutorial-list.md).
 
- toolearn mais informações sobre a gestão de aplicações com o Azure AD, consulte Olá [introdução toosingle início de sessão e gerir o acesso de aplicação no Azure Active Directory](active-directory-appssoaccess-whatis.md).
 
- toolearn mais informações sobre o aprovisionamento de utilizadores, consulte [automatizar o aprovisionamento de utilizadores e desaprovisionamento tooSaaS aplicações](active-directory-saas-app-provisioning.md).

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
