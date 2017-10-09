---
title: "aaaConfigure SSO do Azure AD para aplicações | Microsoft Docs"
description: "Saiba como o serviço de tooself ligar aplicações tooAzure do Active Directory utilizando SAML e SSO baseada em palavra-passe"
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 0d42eb0c-6d3f-4557-9030-e88e86709a19
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.reviewer: luleon
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 002a19a6c7ad25ea2f3b9c6a7c7874ed2be23cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-single-sign-on-tooapplications-that-are-not-in-hello-azure-active-directory-application-gallery"></a>Configurar único início de sessão tooapplications que não estejam na Galeria de aplicações do Azure Active Directory Olá
Este artigo é sobre uma funcionalidade que permite aos administradores tooconfigure único início de sessão tooapplications não está presente na Galeria de aplicações do Azure Active Directory Olá *sem escrever código*. Esta funcionalidade foi lançada a partir do technical preview no 18 de Novembro de 2015 e está incluída no [Azure Active Directory Premium](active-directory-editions.md). Se estiver em vez disso, a procurar orientações para programadores sobre toointegrate aplicações personalizadas com o Azure AD através do código, consulte [cenários de autenticação para o Azure AD](active-directory-authentication-scenarios.md).

Olá Galeria de aplicações do Azure Active Directory fornece uma lista de aplicações que são conhecidos toosupport um formulário de início de sessão no Azure Active Directory, conforme descrito em [neste artigo](active-directory-appssoaccess-whatis.md). Uma vez (como um IT especialista em integrador na sua organização) encontrar aplicação Olá pretende tooconnect, pode começar a utilizar por seguir Olá passo a passo as instruções apresentadas no Olá o Azure management portal tooenable-início de sessão único.

Clientes com [Azure Active Directory Premium](active-directory-editions.md) licenças também obterem estas capacidades adicionais:

* Integração de self-service de qualquer aplicação que suporta SAML 2.0 fornecedores de identidade (iniciado por SP ou iniciadas por IdP)
* Integração de self-service de qualquer aplicação web que tem um baseado em HTML página de início de sessão utilizando [SSO baseada em palavra-passe](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Ligação self-service das aplicações que utilizam o protocolo SCIM Olá para aprovisionamento de utilizadores ([descrito aqui](active-directory-scim-provisioning.md))
* Capacidade tooadd liga tooany aplicação Olá [iniciador da aplicação do Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) ou Olá [painel de acesso do Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)

Isto pode incluir não apenas aplicações de SaaS que utilizar, mas ainda não ter sido integrada toohello Galeria de aplicações do Azure AD, mas as aplicações web de terceiros que a sua organização tiver implementado tooservers que controlar, ou na nuvem de Olá ou no local.

Estas capacidades, também conhecidas como *modelos de integração de aplicação*, forneça pontos de ligação baseada em normas para aplicações que suportam SAML, SCIM ou autenticação baseada em formulários e incluem opções flexíveis e as definições de compatibilidade com um número abrangente de aplicações. 

## <a name="adding-an-unlisted-application"></a>Adicionar uma aplicação não listada
tooconnect uma aplicação utilizando um modelo de integração de aplicações, inicie sessão no portal de gestão do Azure Olá utilizando a sua conta de administrador do Azure Active Directory e procurar toohello **do Active Directory > [Directory] > aplicações**secção, selecione **adicionar**e, em seguida, **adicionar uma aplicação na Galeria de Olá**. 

![][1]

Na Galeria de aplicações de Olá, pode adicionar uma aplicação não listada com Olá **personalizada** categoria Olá esquerda ou selecionando Olá **adicionar uma aplicação não listada** resulta de ligação que é apresentada na pesquisa de Olá se a aplicação pretendida Não foi encontrado. Depois de introduzir um nome para a sua aplicação, pode configurar Olá único início de sessão opções e comportamentos. 

**Sugestão rápida**: como uma melhor prática, utilize Olá pesquisa função toocheck toosee se a aplicação Olá já existe na Galeria de aplicações de Olá. Se encontra-se a aplicação Olá e respetiva descrição menciona suportadas "início de sessão único", em seguida, aplicação Olá já é suportada para federado-início de sessão único. 

![][2]

Adicionar uma aplicação desta forma fornece um toohello experiência muito semelhantes um disponível para aplicações previamente integradas. toostart, selecione **configurar Single Sign-On**. ecrã seguinte Olá apresenta Olá seguintes três opções para configurar o início de sessão único, que são descritos nas Olá secções a seguir.

![][3]

## <a name="azure-ad-single-sign-on"></a>Azure AD início de sessão único
Selecione esta opção tooconfigure baseados em SAML a autenticação para a aplicação Olá. Isto requer que Olá suporte para aplicações SAML 2.0 e deve recolher informações sobre como toouse Olá capacidades SAML da aplicação Olá antes de continuar. Depois de selecionar **seguinte**, será pedido tooenter três diferentes URLs correspondente toohello pontos finais SAML para aplicação Olá. 

![][4]

Nomeadamente:

* **URL de início de sessão (iniciado por SP apenas)** – onde o utilizador Olá fica toothis toosign na aplicação. Se a aplicação Olá está configurada iniciadas por fornecedor único do serviço tooperform início de sessão, em seguida, quando um utilizador navega toothis URL, o fornecedor de serviços de Olá será Olá redirecionamento necessário tooAzure AD tooauthenticate e inicie sessão no utilizador Olá no. Se este campo é preenchido, o Azure AD irá utilizar este URL toolaunch Olá aplicação do Office 365 e Olá painel de acesso do Azure AD. Se este campo é ommited, em seguida, do Azure AD em vez disso, executará o fornecedor de identidade-início de sessão iniciada quando Olá a aplicação é iniciada do Office 365, Olá painel de acesso do Azure AD, ou de Olá do Azure AD único início de sessão no URL (copiable a partir do separador de Dashboard Olá).
* **URL do emissor** -Olá emissor URL deve identificar exclusivamente a aplicação Olá para o qual único início de sessão está a ser configurado. Este é o valor de Olá que o Azure AD envia back tooapplication como Olá **público-alvo** toovalidate esperado é o parâmetro de token SAML Olá e aplicação Olá-lo. Este valor é também apresentado como Olá **ID de entidade** nos metadados qualquer SAML fornecido pela aplicação Olá. Consulte a documentação de SAML da aplicação Olá para obter detalhes sobre o que é o ID de entidade ou valor de audiência está. Abaixo está um exemplo de como Olá URL público-alvo é apresentado na aplicação de token toohello devolvido de SAML Olá:

```
    <Subject>
    <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:unspecificed">chad.smith@example.com</NameID>
        <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
      </Subject>
      <Conditions NotBefore="2014-12-19T01:03:14.278Z" NotOnOrAfter="2014-12-19T02:03:14.278Z">
        <AudienceRestriction>
          <Audience>https://tenant.example.com</Audience>
        </AudienceRestriction>
      </Conditions>
```

* **URL de resposta** -URL de resposta de Olá é onde a aplicação Olá espera token do tooreceive Olá SAML. Este é também referido tooas Olá **URL do serviço de consumidor da asserção (ACS)**. Consulte a documentação de SAML da aplicação Olá para obter detalhes sobre o que é o URL de resposta de tokens de SAML ou o URL de ACS.
  Depois de estes serem introduzidas, clique em **seguinte** tooproceed toohello seguinte ecrã. Este ecrã fornece informações sobre que toobe necessidades configurado no tooenable de lado de aplicação Olá tooaccept num token SAML do Azure AD. 

![][5]

Os valores que são necessários variam consoante a aplicação Olá, por isso, consulte a documentação de SAML da aplicação Olá para obter detalhes. Olá **Sign-On** e **fim de sessão** URL do serviço de ambos os resolver toohello mesmo ponto final, que é o ponto final de processamento de pedidos SAML Olá na sua instância do Azure AD. Olá URL do emissor é o valor de Olá que aparece como Olá "Issuer" dentro Olá aplicação de toohello emitidos token SAML. 

Depois da aplicação tiver sido configurada, clique em **seguinte** botão e, em seguida, Olá **concluída** caixa de diálogo do tooclose Olá. 

## <a name="assigning-users-and-groups-tooyour-saml-application"></a>Atribuir utilizadores e aplicações de SAML tooyour de grupos
Assim que a sua aplicação tiver sido configurado toouse do Azure AD como um fornecedor de identidade baseada em SAML, está quase pronto tootest. Como um controlo de segurança do Azure AD não irá emitir um token, permitindo-lhes toosign numa aplicação Olá, a menos que tenham sido concedidos acesso através do Azure AD. Podem ser concedido acesso a utilizadores diretamente ou através de um grupo que são membros do. 

tooassign um utilizador ou grupo tooyour de aplicação, clique em Olá **atribuir utilizadores** botão. Selecione o utilizador de Olá ou grupo que queira tooassign e, em seguida, selecione Olá **atribuir** botão. 

![][6]

Atribuição de um utilizador permitirá do Azure AD tooissue um token de utilizador de Olá, bem como a causar um mosaico para esta aplicação tooappear no painel de acesso do utilizador Olá. Um mosaico de aplicações também serão apresentados na iniciador da aplicação Olá do Office 365, se o utilizador Olá está a utilizar o Office 365. 

Pode carregar um logótipo de mosaico para aplicação Olá utilizando Olá **carregar o logótipo** botão Olá **configurar** separador aplicação Olá. 

### <a name="customizing-hello-claims-issued-in-hello-saml-token"></a>Personalizar afirmações de Olá emitidas no token SAML Olá
Quando um utilizador efetua a autenticação de aplicação toohello, do Azure AD irá emitir uma aplicação de token toohello SAML que contém informações (ou afirmações) sobre utilizador Olá que identifica exclusivamente. Por predefinição inclui o nome de utilizador Olá, endereço de correio eletrónico, nome próprio e apelido. 

Pode ver ou editar afirmações Olá enviadas em Olá aplicação token toohello SAML Olá **atributos** separador. 

![][7]

Existem duas razões possíveis por que razão poderá necessitar de afirmações de Olá de tooedit emitidas no token SAML Olá: •hello aplicação foi escrita toorequire outro conjunto de afirmação URIs ou afirmações de aplicação de •Your de valores tiver sido implementada de forma que necessita de Olá NameIdentifier afirmações toobe algo que não seja o nome de utilizador Olá (também conhecidas como nome principal do utilizador) armazenados no Azure Active Directory. 

Para obter informações sobre como tooadd e editar afirmações para estes cenários, veja isto [artigo personalização afirmações](active-directory-saml-claims-customization.md). 

### <a name="testing-hello-saml-application"></a>Testar a aplicação de SAML Olá
Assim que tiverem sido configurados Olá URLs de SAML e o certificado no Azure AD e na aplicação Olá, utilizadores ou grupos foram atribuídos toohello aplicação no Azure e Olá afirmações tenham sido revistas e editá-lo se for necessário, em seguida, utilizador de Olá é toosign pronto para Olá aplicação. 

tootest, basta iniciar sessão no Olá painel de acesso do Azure AD em https://myapps.microsoft.com utilizando uma conta de utilizador atribuída toohello aplicação e, em seguida, clique no mosaico de Olá para Olá aplicação tookick desativar Olá único início de sessão no processo. Em alternativa, pode procurar diretamente toohello URL de início de sessão para a aplicação Olá e início de sessão a partir daí. 

Para sugestões de depuração, consulte este [artigo sobre como toodebug baseados em SAML único início de sessão tooapplications](active-directory-saml-debugging.md) 

## <a name="password-single-sign-on"></a>Palavra-passe-início de sessão único
Selecione esta opção tooconfigure [baseada em palavra-passe de início de sessão](active-directory-appssoaccess-whatis.md) para uma aplicação web que tem uma página de início de sessão HTML. SSO baseada em palavra-passe, também referidos tooas palavra-passe vaulting, permite-lhe toomanage acesso e palavras-passe tooweb as aplicações de utilizador que não suportam a Federação de identidade. Também é útil para cenários em que vários utilizadores tem tooshare uma única conta, tais como contas de aplicação da organização tooyour de redes sociais. 

Depois de selecionar **seguinte**, será tooenter pedido Olá URL da baseada na web-página sessão aplicação Olá. Tenha em atenção que tem de ser página Olá que inclua campos entrados Olá nome de utilizador e palavra-passe. Uma vez introduzida, Azure AD inicia uma processo tooparse Olá-página sessão para uma entrada de nome de utilizador e uma entrada de palavra-passe. Se o processo de Olá não for bem sucedido, em seguida,-orienta-o um processo de instalação de uma extensão de browser (requer o Internet Explorer, Chrome ou Firefox) que irá permitir que os campos de Olá de captura toomanually alternativo.

Assim que a página de início de sessão Olá é capturada, podem ser atribuídos a utilizadores e grupos e políticas de credencial podem ser definidas como regular [palavra-passe SSO aplicações](active-directory-appssoaccess-whatis.md).

Nota: Pode carregar um logótipo de mosaico para aplicação Olá utilizando Olá **carregar o logótipo** botão Olá **configurar** separador aplicação Olá. 

## <a name="existing-single-sign-on"></a>Existente Single Sign-On
Selecione esta opção tooadd portal de uma ligação tooan aplicação tooyour organização painel de acesso do Azure AD ou o Office 365. Pode utilizar este tooadd ligações toocustom as aplicações web que a utilizam atualmente os serviços de Federação do Active Directory do Azure (ou outro serviço de Federação) em vez do Azure AD para autenticação. Em alternativa, pode adicionar as páginas do ligações avançadas toospecific SharePoint ou outras páginas web que deseje tooappear nos painéis de acesso do utilizador. 

Depois de selecionar **seguinte**, será pedido tooenter Olá URL de Olá aplicação toolink para. Depois de concluída, utilizadores e grupos que podem ser atribuídos toohello aplicação, o que faz com que Olá aplicação tooappear no Olá [iniciador da aplicação do Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) ou Olá [painel de acesso do Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) para os utilizadores.

Nota: Pode carregar um logótipo de mosaico para aplicação Olá utilizando Olá **carregar o logótipo** botão Olá **configurar** separador aplicação Olá.

## <a name="related-articles"></a>Artigos relacionados
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](active-directory-apps-index.md)
* [Como tooCustomize as afirmações emitidas no hello SAML Token para aplicações de Pre-Integrated](active-directory-saml-claims-customization.md)
* [Resolução de problemas baseados em SAML Single Sign-On](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saas-custom-apps/customapp1.png
[2]: ./media/active-directory-saas-custom-apps/customapp2.png
[3]: ./media/active-directory-saas-custom-apps/customapp3.png
[4]: ./media/active-directory-saas-custom-apps/customapp4.png
[5]: ./media/active-directory-saas-custom-apps/customapp5.png
[6]: ./media/active-directory-saas-custom-apps/customapp6.png
[7]: ./media/active-directory-saas-custom-apps/customapp7.png
