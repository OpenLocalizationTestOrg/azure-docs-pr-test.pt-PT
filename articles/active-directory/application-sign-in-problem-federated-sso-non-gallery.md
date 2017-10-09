---
title: "aaaProblems início de sessão na aplicação de Galeria não tooa configurada para Federado de sessão único-| Microsoft Docs"
description: "Orientações para problemas específicos de Olá poderá enfrentam quando iniciar sessão na aplicação tooan configurada para baseados em SAML federado-início de sessão único com o Azure AD"
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
ms.openlocfilehash: 1243456695c097f404a66fc89893efa2afdaaf22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-non-gallery-application-configured-for-federated-single-sign-on"></a>Problemas de início de sessão na aplicação de Galeria não tooa configurada para federado-início de sessão único

tootroubleshoot o problema, tem de configuração da aplicação Olá tooverify no Azure AD como seguir:

-   Seguiu todos os passos de configuração de Olá de Olá aplicação de galeria do Azure AD.

-   corresponder estes valores esperados na aplicação Olá Olá identificador e o URL de resposta configurado no AAD

-   Atribuiu utilizadores toohello aplicação

## <a name="application-not-found-in-directory"></a>Não foi encontrada no diretório de aplicação

*AADSTS70001 de erro: A aplicação com o identificador 'https://contoso.com' não foi encontrada no diretório de Olá*.

**Uma causa possível**

atributo de emissor Olá envia de Olá aplicação tooAzure que AD no pedido SAML Olá não corresponde ao valor do identificador de Olá configurado na aplicação Olá do Azure AD.

**Resolução**

Certifique-se esse atributo de emissor Olá no pedido SAML Olá correspondência Olá valor do identificador configurado no Azure AD:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.

   * Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**

6.  Selecione aplicação Olá pretende tooconfigure-início de sessão único.

7.  Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.

8.  <span id="_Hlk477190042" class="anchor"></span>Aceda demasiado**domínios e URLs** secção. Certifique-se de que o valor na caixa de texto valor Olá para o valor do identificador de Olá apresentado no registo de erros Olá correspondência de identificador de Olá Olá.

Depois de ter atualizado o valor do identificador de Olá no Azure AD e de Olá valor correspondente envia pela aplicação Olá no pedido SAML Olá, deve ser capaz de toosign na aplicação toohello.

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a>endereço de resposta de Olá não correspondem aos endereços de resposta de Olá configurados para a aplicação Olá. 

*AADSTS50011 de erro: o endereço de resposta de Olá 'https://contoso.com' não correspondem aos endereços de resposta de Olá configurados para a aplicação Olá* 

**Uma causa possível** 

Olá AssertionConsumerServiceURL valor no pedido SAML Olá não corresponde ao valor de URL de resposta de Olá ou padrão configurado no Azure AD. Olá AssertionConsumerServiceURL valor no pedido SAML Olá é URL Olá, consulte o erro de Olá. 

**Resolução** 

Certifique-se de que o valor AssertionConsumerServiceURL Olá no pedido SAML Olá de correspondente Olá valor do URL de resposta configurado no Azure AD. 
 
1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.** 

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá. 

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item. 

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory. 

5.  Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações. 

  * Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**
  
6.  Selecionar aplicação Olá pretende tooconfigure-início de sessão único

7.  Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.

8.  Aceda demasiado**domínios e URLs** secção. Certifique-se ou Atualize o valor Olá Olá de toomatch AssertionConsumerServiceURL valor no pedido SAML Olá do Olá URL de resposta caixa de texto.

  * Se não vir a caixa de texto de URL de resposta de Olá, selecione Olá **Mostrar avançadas definições de URL** caixa de verificação. 

Depois de ter atualizado o valor do URL de resposta de Olá no Azure AD e tem de correspondência do valor de Olá envia pela aplicação Olá em Olá pedido SAML, deve ser capaz de toosign na aplicação toohello.

## <a name="user-not-assigned-a-role"></a>Não atribuído uma função de utilizador

*Erro AADSTS50105: Olá com sessão iniciada utilizador 'brian@contoso.com' não está atribuído a função de tooa para aplicação Olá*

**Uma causa possível**

Olá tem não foi concedido ao utilizador acesso toohello aplicação no Azure AD.

**Resolução**

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

Após um curto período de tempo, os utilizadores Olá que selecionou de ser capaz de toolaunch estas aplicações utilizando Olá métodos descritos na secção de descrição de solução Olá.

## <a name="not-a-valid-saml-request"></a>Não um pedido de SAML válido

*Erro AADSTS75005: Olá do pedido não é uma mensagem de protocolo Saml2 válida.*

**Uma causa possível**

Azure AD não suporta Olá SAML do pedido enviados pela aplicação Olá para o início de sessão único. Alguns problemas comuns são:

-   Campos necessários no pedido SAML Olá em falta

-   Método de pedido codificado de SAML

**Resolução**

1.  Capture pedido SAML. Siga o tutorial Olá no [como toodebug baseados em SAML único início de sessão tooapplications no Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn como toocapture Olá SAML do pedido.

2.  Contacte o fabricante da aplicação Olá e partilha:

    -   Pedido SAML

    -   [Requisitos de protocolo do Azure AD único início de sessão SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

Eles devem validar que suportam a implementação do Azure AD SAML Olá para o início de sessão único.

## <a name="no-resource-in-requiredresourceaccess-list"></a>Nenhum recurso na lista de requiredResourceAccess

*Erro AADSTS65005: aplicação de cliente de Olá pediu acesso tooresource ' 00000002-0000-0000-c000-000000000000'. Este pedido falhou porque o cliente de Olá não especificou este recurso na lista de requiredResourceAccess*.

**Uma causa possível**

objeto da aplicação Olá está danificado.

**Resolução**

problema de Olá toosolve, remover Olá aplicação do diretório de Olá. Em seguida, adicionar e reconfigurar aplicação Olá, siga os passos de Olá abaixo:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.

  * Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**

6.  Selecione aplicação Olá pretende tooconfigure-início de sessão único.

7.  Clique em **eliminar** em Olá superior esquerdo da aplicação Olá **descrição geral** painel.

8.  Atualizar do Azure AD e adicionar aplicação Olá da galeria do Azure AD Olá. Em seguida, Configure novamente a aplicação Olá.

Após a reconfiguração da aplicação Olá, deve ser capaz de toosign na aplicação toohello.

## <a name="certificate-or-key-not-configured"></a>Certificado ou chave não configurado

Erro AADSTS50003: Nenhuma chave de assinatura configurado.

**Uma causa possível**

objeto da aplicação Olá está danificado e do Azure AD não reconhece o certificado de Olá configurado para a aplicação Olá.

**Resolução**

toodelete e criar um novo certificado, siga os passos de Olá abaixo:

1.  Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**

2.  Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.

3.  Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.

4.  Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.

5.  Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.

  * Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**

6.  Selecione aplicação Olá pretende tooconfigure-início de sessão único.

7.  Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.

8.  Clique em **criar novo certificado** em Olá **SAML certificado de assinatura** secção.

9.  Selecione a data de expiração. Em seguida, clique em **guardar.**

10. Verifique **tornar o novo certificado ativa** certificado do toooverride Olá Active Directory. Em seguida, clique em **guardar** , Olá parte superior do painel de Olá e aceitar o certificado de rollover de Olá tooactivate.

11. Em Olá **certificado de assinatura de SAML** secção, clique em **remover** tooremove Olá **não utilizados** certificado.

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a>Problema ao personalizar Olá SAML afirmações enviadas tooan aplicação

toolearn como afirmações de atributo do toocustomize Olá SAML enviada tooyour aplicação, consulte [afirmações mapeamento no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.

## <a name="next-steps"></a>Passos seguintes
[Requisitos de protocolo do Azure AD único início de sessão SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
